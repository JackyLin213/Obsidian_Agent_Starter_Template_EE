---
title: "<% tp.file.title %>"
type: permanent
status: evergreen
tags:
  - Resource/Tool
  - Tool/<% tp.file.title.replace(/\s+/g, '_') %>
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
category: "實驗室儀器" # 實驗室儀器 | EDA軟體 | 模擬工具 | 效率軟體 | 開發工具 | 雲端服務
model_or_version: ""
vendor_or_maker: ""
pricing: "買斷制" # 免費開源 | 訂閱制 | 買斷制 | 實驗室公用
location_or_asset_id: "硬體實驗室" # 存放位置 / 資產編號
calibration_cycle: "每年" # 不需校準 | 每季 | 每半年 | 每年
last_calibrated: "YYYY-MM-DD"
next_calibration: "YYYY-MM-DD"
calibration_status: "🟢 Valid" # 🟢 Valid | 🟡 Due Soon | 🔴 Expired | N/A
official_url: ""
documentation_url: ""
aliases: []
sources: []
up: "[[30_Resources/03_MOCs/MOC - 工具與技術選型]]"
---

# 🛠️ <% tp.file.title %>

> [!SUMMARY] 🛠️ 工具與儀器全景速讀 (30s Scannability)
> - 🏷️ **工具類別**：`category` | **廠牌 / 型號**：`vendor_or_maker` `model_or_version`
> - 📍 **位置 / 資產號**：`location_or_asset_id` | **授權與費用**：`pricing`
> - 🎯 **校準狀態**：`calibration_status` (下次校準: `next_calibration`)
> - 🌐 **官方與文檔入口**：`official_url` | `documentation_url`

---

## 1. 💡 一句話定位與核心價值 (Core Value Proposition)

> [!ABSTRACT] 核心定位
> 簡潔描述本工具/儀器在硬體系統研發與日常工作中的關鍵定位與不可替代性。

---

## 2. ⚡ 規格參數與極限額定值 (Specifications & Maximum Ratings)

| 關鍵參數 (Parameter) | 規格數值 (Rating / Spec) | 備註說明 / 極限限制 (AMR) |
| :--- | :--- | :--- |
| **工作頻寬 / 採樣率** | | |
| **通道數 / 探棒配置** | | |
| **輸入阻抗與耦合** | 1MΩ / 50Ω | |
| **最大耐受電壓 (AMR)** | ⚠️ 嚴禁超過： | 💥 超額將損壞前端放大電路！ |
| **支援通訊介面 / 協定** | USB / GPIB / LAN (LXI) | |

---

## 3. 🛡️ 安全操作規範與防呆標準 (Operating SOP & ESD Safety)

> [!CAUTION] 🚨 實驗室量測防呆與安全警告
> 1. **防靜電保護 (ESD)**：接觸儀器與待測物 (DUT) 前必須配戴防靜電手環，並確認接地良好。
> 2. **輸入過載保護**：量測高壓或高 $di/dt$ 節點前，必須預先將衰減比調整至 10:1 或 100:1。
> 3. **探棒校準 (Probe Compensation)**：更換被動探棒後，必須在標準 1kHz 參考信號進行低頻補償調整，確保平坦方波。

- [ ] **開機與自我檢測程序**：
- [ ] **探棒接地手法標準**：優先採用接地彈簧 (Ground Spring) 或同軸短線，禁止使用長鱷魚夾量測高頻/漣波。
- [ ] **關機與收納標準**：

---

## 4. ⚖️ 優缺點與適用場景評估 (Pros, Cons & Applications)

### 🟢 核心優勢 (Pros)
- 

### 🔴 劣勢與限制 (Cons)
- 

### 🎯 最佳適用情境 vs 禁忌場景 (Best vs Worst Use Cases)
- 🟢 **推薦場景**：
- 🔴 **不建議場景**：

---

## 5. 💻 常用設定、腳本與自動化代碼 (Configuration, SCPI & Scripts)

### 5.1 常用快捷操作與預設設定
- 

### 5.2 自動化控制代碼片段 (SCPI / Python Automation)
```python
import pyvisa

# 初始化 VISA 資源管理器
rm = pyvisa.ResourceManager()
# 連接儀器 (請替換為實際 VISA 位址)
inst = rm.open_resource("TCPIP0::192.168.1.100::inst0::INSTR")
inst.timeout = 5000

# 讀取儀器 IDN
print("Connected to:", inst.query("*IDN?"))

# 常用 SCPI 量測配置
inst.write(":AUToscale")
```

---

## 6. 📅 校準紀錄與維護歷史 (Calibration & Maintenance History)

| 校準日期 | 校準單位 / 報告編號 | 結果判定 | 下次到期日 | 經辦人 |
| :---: | :--- | :---: | :---: | :---: |
| `last_calibrated` | 內部自校 / 原廠校驗 | `calibration_status` | `next_calibration` | |

---

## 7. 🔗 知識庫中關聯的專案與除錯筆記 (Related Projects & Debug Notes)

```dataview
TABLE project AS "專案", board_rev AS "版本", severity AS "嚴重度"
FROM "30_Resources/02_Permanent/Hardware/Debug"
WHERE contains(instruments, "<% tp.file.title %>") OR contains(file.text, "<% tp.file.title %>")
SORT file.mtime DESC
LIMIT 10
```

- 關聯專案：`[[專案名稱]]`
- 關聯概念：`[[概念卡片]]`
