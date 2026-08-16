---
title: "<% tp.file.title %>"
type: permanent
status: evergreen
tags:
  - Software/Pattern
  - Software/Snippet/C # 請替換: C | Cpp | Python | Rust | TypeScript | Go | Verilog
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
language: "C" # C | C++ | Python | Rust | TypeScript | Go | Verilog
pattern_type: "Concurrency" # Concurrency | Memory | DataStructure | DesignPattern | Bitwise | Algorithmic
time_complexity: "O(1)"
space_complexity: "O(1)"
thread_safe: true
aliases: []
sources: []
up: "[[30_Resources/03_MOCs/MOC - 軟體系統工程總索引]]"
---

# 💻 <% tp.file.title %>

> [!QUOTE] 💡 核心模式與語意定義 (Core Pattern Statement)
> 用一句話精煉本代碼模式/演算法的本質與解決的核心計算/並發問題。

> [!TIP] ⚡ 複雜度與經驗法則 (Rule of Thumb & Complexity)
> - **時間複雜度**：$T(N) = \text{time\_complexity}$ ｜ **空間複雜度**：$S(N) = \text{space\_complexity}$
> - **執行緒安全 (Thread-Safety)**：`thread_safe` ｜ **適用場景**：高頻調用 / 嵌入式低延遲

---

## 1. 💡 問題情境與模式動機 (Motivation & Context)

- **適用場景**：(如：單生產者-單消費者 SPSC 無鎖隊列、環形緩衝區 Ring Buffer、位元翻轉運算)
- **傳統作法痛點**：(如：Mutex 鎖競爭導致上下文中斷切換延遲過高)

---

## 2. 💻 慣用代碼實現 (Idiomatic Implementation)

```c
#include <stdint.h>
#include <stdbool.h>
#include <stdatomic.h>

#define RING_BUFFER_SIZE 1024 // 必須為 2 的冪次方

typedef struct {
    uint8_t buffer[RING_BUFFER_SIZE];
    atomic_size_t head;
    atomic_size_t tail;
} lockfree_ring_buffer_t;

bool ring_buffer_push(lockfree_ring_buffer_t *rb, uint8_t data) {
    size_t head = atomic_load_explicit(&rb->head, memory_order_relaxed);
    size_t next_head = (head + 1) & (RING_BUFFER_SIZE - 1);
    
    if (next_head == atomic_load_explicit(&rb->tail, memory_order_acquire)) {
        return false; // Buffer Full
    }
    
    rb->buffer[head] = data;
    atomic_store_explicit(&rb->head, next_head, memory_order_release);
    return true;
}
```

---

## 3. 📐 複雜度與效能特徵 (Complexity & Performance Analysis)

- **時間複雜度推導**：
  $$T(N) = \mathcal{O}(1)$$
  *藉由二進位遮罩 `& (SIZE - 1)` 替代耗時的取模運算 `%`，大幅壓低 CPU 指令週期。*
- **空間與記憶體對齊 (Memory Alignment & Cache Line)**：
  *需注意 `head` 與 `tail` 應配置於不同 Cache Line（使用 `alignas(64)`），防止偽共享 (False Sharing) 性能崩潰。*

---

## 4. ⚠️ 關鍵邊界條件與致命陷阱 (Edge Cases & Pitfalls)

| 邊界/極端條件 | 潛在致命陷阱 (Pitfall) | 正確防禦作法 |
| :--- | :--- | :--- |
| **緩衝區滿 (Buffer Full)** | 覆寫未讀取的舊數據造成資料損毀 | 檢查 `next_head == tail` 並返回 `false` |
| **多生產者同時寫入** | 本實現為 SPSC (單寫單讀)，多寫入者將破壞原子性 | 若需 MPMC，改用 CAS (Compare-And-Swap) 迴圈 |
| **編譯器指令重排** | 缺乏 Memory Barrier 導致數據尚未寫入即更新指標 | 嚴格使用 `memory_order_release` 與 `acquire` |

---

## 5. 🧪 測試用例與驗證 (Unit Test & Benchmark)

```c
void test_ring_buffer_basic(void) {
    lockfree_ring_buffer_t rb = {0};
    assert(ring_buffer_push(&rb, 0xAA) == true);
    // 斷言邏輯...
}
```

---

## 6. 🔗 語意網絡關聯 (Semantic Connections)
- ⬆️ **上位主題**：`[[30_Resources/03_MOCs/MOC - 軟體系統工程總索引]]`
- ↔️ **相關模式**：`[[雙緩衝機制與零拷貝隊列]]`
- ⬇️ **實戰應用**：`[[Template - Firmware Driver Spec]]`
