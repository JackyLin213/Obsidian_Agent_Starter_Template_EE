---
title: "<% tp.file.title %>"
type: literature
status: draft # draft | processing | processed | archived
tags:
  - Literature/AppNote # 可選: Literature/AppNote | Literature/WhitePaper | Literature/Article | Literature/Datasheet
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
author_vendor: "TI" # 原廠或作者: TI | ADI | MPS | Infineon | NXP | Qualcomm | Intel
doc_id: "" # 原廠文件編號 (如 SLVA001 / AN-1148 / WP-021)
published_year: "<% tp.date.now('YYYY') %>"
url: ""
rating: 4 # 1~5 星評級
category: "Power" # Power | SIPI | PCB | Components | Thermal | RF | MCU
aliases: []
sources: []
up: "[[30_Resources/03_MOCs/MOC - 知識索引]]"
---

# 📖 <% tp.file.title %>

> [!ABSTRACT] ⚡ 30 秒文獻精華速讀 (Executive Summary / TL;DR)
> - 🎯 **核心宗旨 / 欲解決問題**：
> - 💡 **核心結論 / 設計準則精要**：
> - 📐 **適用電路拓撲與應用場景**：
> - ⚠️ **關鍵設計陷阱與邊界風險 (Gotchas)**：

> [!INFO] 📋 文獻基本檔案 (Document Profile)
> - **原廠 / 作者**：`author_vendor`
> - **文件單號**：`doc_id`（出版年份：`published_year`）
> - **技術領域**：`category` | **精讀推薦度**：⭐⭐⭐⭐
> - **官方原始文件連結**：[原廠手冊 / App Note 線上網址](`url`)

---

## 1. ⚙️ 核心電路拓撲與物理工作機制 (Circuit Topology & Physics)

### 1.1 電路架構與等效模型 (Topology & Equivalent Circuit)
```
          L_filter          V_OUT
  SW ───────/\/\/\/\/───┬─────
                        │
                       === C_OUT
                        │
  GND ──────────────────┴───── GND
```
- **工作機制解析**：
- 

### 1.2 核心控制方程與物理參數 (Key Equations & Parameters)
- **主設計公式**：
  $$\Delta I_L = \frac{V_{IN} - V_{OUT}}{L \cdot f_{sw}} \cdot \frac{V_{OUT}}{V_{IN}}$$
- **參數定義與邊界說明**：
  - $\Delta I_L$：電感紋波電流峰峰值 ($A$)，通常設計為最大輸出電流的 $20\% \sim 40\%$。
  - $L$：功率電感感值 ($H$)。
  - $f_{sw}$：開關頻率 ($\text{Hz}$)。

---

## 2. 📐 關鍵設計步驟與元件計算 (Step-by-Step Design & Sizing)

### 2.1 標準設計計算流程 (Design Workflow)
1. **確定系統輸入/輸出規格**：$V_{IN(min)}, V_{IN(max)}, V_{OUT}, I_{OUT(max)}, \Delta V_{OUT}$
2. **計算功率電感感值與飽和電流**：$I_{sat} \ge I_{OUT(max)} + \frac{\Delta I_L}{2}$
3. **計算輸出去耦電容容量與 ESR 限制**：
4. **環路補償與反饋網絡計算**：

### 2.2 🛡️ 4 大硬體審查規範檢核 (EE Review Criteria)
- [ ] **最壞情況分析與降額 (Derating)**：電容耐壓降額 $\le 75\%$，MOSFET 功率熱降額 $\le 60\%$，結溫 $T_J \le 105^\circ\text{C}$。
- [ ] **訊號完整性與回流路徑 (SI Return Path)**：敏感反饋走線 (FB/COMP) 遠離高頻開關噪訊節點 (SW)。
- [ ] **電源分配網絡與噪訊抑制 (PDN & Loops)**：高 $di/dt$ 輸入去耦迴路面積最小化，緊貼晶片引腳。
- [ ] **無損除錯與可測試性 (Testability)**：預留關鍵電壓與開關節點測試點 (Test Points)。

---

## 3. 🛡️ PCB Layout 與實戰佈線守則 (Layout & SI/PI Best Practices)

### 3.1 佈局與走線黃金法則 (DOs & DON'Ts)
| 類別 | 推薦做法 (DOs) | 致命禁忌 (DON'Ts) |
| :--- | :--- | :--- |
| **高頻開關迴路** | 輸入電容接地端與晶片 PGND 緊鄰打地孔 | ❌ 走線繞行過長，形成大面積輻射天線 |
| **敏感反饋走線 (FB)**| 緊貼地平面走線，遠離電感與開關節點 SW | ❌ FB 走線平行穿越 SW 鋪銅正下方 |
| **散熱焊盤 (Thermal)**| 晶片底部打滿密集散熱過孔連接至內層 GND | ❌ 散熱焊盤開窗不足導致局部熱積聚 |

---

## 4. 🚫 常見設計陷阱與除錯避坑 (Pitfalls & Gotchas)

> [!WARNING] ⚠️ 原廠沒明說但工程師常踩的坑
> 1. **陶瓷電容直流偏壓效應 (DC Bias Effect)**：高壓下 MLCC 實際容值可能衰減達 $50\%\sim 70\%$，導致輸出紋波超標與環路不穩。
> 2. **輕載跳頻噪訊 (Light-Load PFM Ripple)**：進入省電模式時紋波頻率掉入音訊區間引發嘯叫。
> 3. **寄生電感引發的開關振鈴 (SW Ringing)**：PCB 走線寄生電感導致過沖超過晶片 AMR 絕對耐壓。

---

## 5. 💎 Zettelkasten 原子卡片沉澱 (Permanent Notes Distilled)

> [!TIP] 💡 原子化蒸餾指南
> 將本篇文獻提煉出的通用定理、電路機制與設計準則，獨立沉澱為 2~5 張永久原子卡片，存入 `30_Resources/02_Permanent/Hardware/` 對應三階子目錄中。

- [ ] `[[30_Resources/02_Permanent/Hardware/Power/降壓電路電感飽和電流計算與降額準則]]`：從本 App Note 第 4 節提煉之電感選型計算通用法則。
- [ ] `[[30_Resources/02_Permanent/Hardware/PCB/DCDC高頻開關迴路PCB佈局黃金法則]]`：高 $di/dt$ 迴路最小化實務佈線標準。
- [ ] `[[30_Resources/02_Permanent/Hardware/Components/MLCC直流偏壓特性對電源紋波之影響]]`：電容選型必備降額知識。

---

## 6. 📦 收集箱處理狀態與封存 (Inbox Zero Protocol)

> [!SUCCESS] 📦 處理完成後之封存標記 (Processed Callout)
> 當完成本篇文獻之重點提煉與原子卡片沉澱後：
> 1. 將 Frontmatter `status` 改為 `processed`。
> 2. 原始剪藏若位於 `00_Inbox/Clippings/`，可安全移至 `40_Archives/Inbox_History/`。

---

## 7. 🔍 智慧動態反向關聯 (Backlinks Explorer)

```dataview
TABLE file.folder AS "所屬目錄", type AS "類型", status AS "狀態", file.mtime AS "最後更新"
FROM [[]]
WHERE file.name != this.file.name
SORT file.mtime DESC
LIMIT 10
```
