---
title: "<% tp.file.title %>"
type: permanent
status: evergreen # draft | processing | evergreen | archived
tags:
  - Hardware/SIPI # 請依主題替換: Hardware/SIPI | Hardware/Power | Hardware/PCB | Hardware/Components | Domain/Topic
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
aliases: []
sources: []
up: "[[30_Resources/03_MOCs/MOC - 所屬主題]]"
---

# 💎 <% tp.file.title %>

> [!QUOTE] 💡 核心本質定義 (Core Principle)
> 用一句話精煉定義本概念的底層本質（自洽、精確、去情境化）。

> [!TIP] ⚡ 工程直覺與經驗法則 (Rule of Thumb / Mental Model)
> 一句話直覺心智模型與實務經驗數值（如：*「高頻電流永遠走電感最小路徑；3W 走線間距可壓制 70% 串擾；50 mil 寬走線約有 1nH/inch 寄生電感」*）。

---

## 1. ⚙️ 物理機制與數學建模 (Physics & Mathematical Modeling)

### 1.1 第一性原理與底層機制 (Physics & First Principles)
- 闡述電磁場、能量流動、載流子行為或電路拓撲的底層物理規律：
- 

### 1.2 數學模型與核心控制方程 (Equations & Formulas)
- **主控制方程**：
  $$Z_0 = \frac{87}{\sqrt{\varepsilon_r + 1.41}} \ln\left(\frac{5.98h}{0.8w + t}\right)$$
- **參數物理意義與單位**：
  - $Z_0$：特性阻抗 ($\Omega$)
  - $\varepsilon_r$：介質相對介電常數 (Relative Permittivity)
  - $h, w, t$：介質厚度、線寬、銅厚 ($\text{mil}$ 或 $\text{mm}$)

### 1.3 等效電路模型與架構示意 (Equivalent Circuit / Diagram)
```
         L_trace
  IN ───/\/\/\/\/────┬────────── OUT
                     │
                    === C_parasitic
                     │
  GND ───────────────┴────────── GND
```

---

## 2. 🚀 工程設計準則與正反模式 (Design Rules & Anti-Patterns)

### 2.1 ✅ 推薦設計準則 (Best Practices & DOs)
- [ ] **DO 1 (佈線/佈局)**：
- [ ] **DO 2 (接地與屏蔽)**：
- [ ] **DO 3 (參數裕度)**：

### 2.2 🚫 致命反模式 (Deadly Anti-Patterns & DON'Ts)
- [ ] ❌ **DON'T 1 (常見設計陷阱)**：
- [ ] ❌ **DON'T 2 (量測與驗證盲點)**：

### 2.3 🔄 工程權衡與折衷考量 (Engineering Trade-offs)
| 決策方向 | 獲得效益 (Pros) | 付出代價 (Cons) | 推薦折衷準則 |
| :--- | :--- | :--- | :--- |
| **方案 A** | 抑制噪訊與振鈴 | 增加 BOM 成本與佔板面積 | 關鍵高頻節點採用 |
| **方案 B** | 極致精簡空間與成本 | 裕度較低，易受寄生效應干擾 | 次要非關鍵線路採用 |

---

## 3. ⚖️ 邊界條件與失效極限 (Boundary Conditions & Breakdown Limits)

> [!WARNING] ⚠️ 模型失效臨界點 (Breakdown Limits)
> - **適用範圍 (Valid Region)**：
> - **何時失效 (When it Fails)**：在何種頻率、上升時間 ($t_r$)、溫度或尺度下，本模型/經驗公式將失效？
>   *(例如：當信號上升沿時間 $t_r < 6 \times T_{pd}$ 走線延遲時，集總參數模型失效，必須導入分佈參數傳輸線模型)*

---

## 4. 🔗 四維語意網絡 (4D Semantic Web)

- ⬆️ **上位宏觀理論 (Broader Theory / MOC)**：
  - `[[30_Resources/03_MOCs/MOC - 所屬主題]]`
- ↔️ **同級平行概念 (Related Concepts)**：
  - `[[相關原子永久卡片A]]`
  - `[[相關原子永久卡片B]]`
- ⬇️ **下位應用與實證案例 (Instances & Empirical Data)**：
  - 晶片選型卡：`[[TPS546D24A 12A 電源晶片規格與 Layout 避坑指南]]`
  - 除錯實驗記錄：`[[Debug - 12V轉1V0電源紋波過大問題排查]]`
  - 研發專案：`[[10_Projects/2026-新一代邊緣計算主板研發專案]]`
- 📚 **來源文獻 (Source Literature)**：
  - `[[@Bogatin_2020_SignalAndPowerIntegritySimplified]]`

---

## 5. 🔍 智慧動態反向關聯 (Backlinks Explorer)

```dataview
TABLE file.folder AS "所屬目錄", type AS "類型", status AS "狀態", file.mtime AS "最後更新"
FROM [[]]
WHERE file.name != this.file.name
SORT file.mtime DESC
LIMIT 10
```
