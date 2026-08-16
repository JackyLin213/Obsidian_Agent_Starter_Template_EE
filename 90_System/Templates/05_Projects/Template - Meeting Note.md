---
title: "<% tp.file.title %>"
type: area
status: completed
tags:
  - Meeting
  - Meeting/HardwareReview
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
date: "<% tp.date.now('YYYY-MM-DD') %>"
project: "[[10_Projects/專案名稱]]"
meeting_type: "Schematic Review" # Schematic Review | Layout Review | EVT Bring-up Sync | Vendor/FAE Alignment | Weekly Sync | Post-Mortem
chair: "[[人物名稱]]"
attendees:
  - "[[人物名稱]]"
location: "線上會議 (Google Meet)" # 線上會議 | 實驗室 302 | 會議室 A
review_verdict: "CONDITIONAL PASS" # PASS | CONDITIONAL PASS | REJECT | FOR_INFO_ONLY
action_item_count: 0
aliases: []
sources: []
up: "[[20_Areas/日誌]]"
---

# 👥 <% tp.file.title %>

> [!IMPORTANT] ⚡ 30 秒評審結論與關鍵摘要 (Executive Summary)
> - **評審結論**：`review_verdict`
> - **核心共識**：一句話總結本次會議達成的最核心共識或階段性結論。
> - **緊急阻礙點 (Critical Blockers)**：標記是否引發阻礙或需進行 PCB 改版 ECO。
> - **會議基本資訊**：📅 **日期**：`date` ｜ 🏢 **地點**：`location` ｜ 👤 **主席**：`chair` ｜ 🎯 **專案**：`project`

---

## 👥 參與人員與職責 (Attendees)
- **硬體架構/設計 (EE)**：`chair`、
- **PCB Layout 工程師**：
- **韌體/軟體支援 (FW/SW)**：
- **外部原廠/供應商 FAE**：

---

## 🎯 會議議程與目標 (Agenda & Objectives)
1. 
2. 
3. 

---

## 🔬 硬體工程審查與技術討論記錄 (Hardware Technical Discussion)

### 議題 1：[模組名稱/電路功能] 評審與設計檢查
- **當前設計狀態**：
- **審查發現點 (Findings)**：
  - *最壞情況與降額*：
  - *回流路徑與阻抗*：
  - *PDN 去耦與迴路面積*：
- **討論與結論**：

### 議題 2：[技術分歧或架構評估]
- 🗣️ **分歧點與各方立場**：
  - **方案 A (EE 主張)**：
  - **方案 B (Layout / 結構主張)**：
- ⚖️ **折衷權衡依據**：
- 📌 **最終定案**：

---

## ⚖️ 正式達成之決策 (Key Decisions Made)
> 若涉及重大架構變更，需同步建立 ADR 決策卡片。

- 📌 **決策 1**：描述決策內容與生效範圍 ➡️ *衍生 ADR: [[ADR - 決策主題]]*
- 📌 **決策 2**：描述決策內容與生效範圍

---

## ✅ 會後行動待辦矩陣 (Action Items)

| 狀態 | 負責人 | 具體任務與交付成果 (Deliverable) | 優先級 | 截止日 (Deadline) | 追蹤 Issue / 備註 |
| :---: | :--- | :--- | :---: | :---: | :--- |
| [ ] | 👤 @名稱 | 修改 DCDC 輸出反饋分壓電阻阻值，滿足結溫降額 | P0 | YYYY-MM-DD | [[Issue-01]] |
| [ ] | 👤 @名稱 | 在換層過孔兩側補齊 GND Stitching Vias 並重新輸出 Gerber | P1 | YYYY-MM-DD | ECO-001 |
| [ ] | 👤 @名稱 | 向 TI FAE 索取 PMIC 滿載熱阻模型 $R_{\theta JA}$ 數據 | P2 | YYYY-MM-DD | |

---

## 📎 相關參考附件與波形圖紙 (Attachments & References)
- 原理圖圖紙：`[[90_System/Attachments/]]`
- 示波器波形 / 測試數據：`[[90_System/Attachments/]]`
- 原廠 Datasheet / AppNote：`[[30_Resources/01_Literature/]]`
