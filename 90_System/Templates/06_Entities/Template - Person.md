---
title: "<% tp.file.title %>"
type: area
status: active
tags:
  - People/Contact
  - People/<% tp.file.title.replace(/\s+/g, '_') %>
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
category: "原廠FAE" # 原廠FAE | 代理商業務 | 協力廠商 | 團隊成員 | 跨部門夥伴 | 業界導師 | 客戶
company: ""
role: ""
location: ""
email: ""
phone: ""
line_wechat: ""
contact_frequency: "每月" # 每週 | 每月 | 每季 | 每年
last_contacted: "<% tp.date.now('YYYY-MM-DD') %>"
next_followup: ""
nda_signed: false
aliases: []
sources: []
up: "[[20_Areas/人際網絡]]"
---

# 👤 <% tp.file.title %>

> [!INFO] 📋 個人與商務 CRM 概覽 (30s Scannability)
> - 🏢 **公司 / 組織**：`company`
> - 💼 **職稱 / 角色**：`role`
> - 🏷️ **關係定位**：`category`
> - ⏱️ **維護頻率**：`contact_frequency` | **上次對接**：`last_contacted`
> - 📅 **下次預定跟進**：`next_followup`
> - 🔒 **NDA / 協議狀態**：`nda_signed`

---

## 1. 🌟 背景檔案與專長領域 (Profile & Expertise)

### 1.1 基本資料與聯繫方式
- **電子郵件**：`email`
- **聯絡電話**：`phone`
- **即時通訊 (LINE/WeChat)**：`line_wechat`
- **辦公地點 / 常駐地**：`location`

### 1.2 核心專長與背景
- **專長技術領域**：
- **溝通風格與偏好**：(例如：偏好 Email 寄送規格書、訊息回覆快速、需事先預約會議)
- **共同話題 / 興趣偏好**：
- **重要紀念日 / 備忘**：

---

## 2. ⚡ 硬體商務與技術對接資訊 (Vendor & Technical Support)

> [!TIP] 💡 原廠/代理商/協力廠技術支援通道
> 專為硬體工程師維護之供應鏈與技術支援資訊。

| 支援項目 | 詳細說明 |
| :--- | :--- |
| **負責產品線 / 晶片系列** | |
| **樣品 (Sample) / EVB 申請** | 流程： |
| **原廠 FAE / 設計審查支援** | 支援範疇：Schematic Review / Layout Review / 實驗室量測 |
| **機密資料 / NDA 狀態** | |
| **代理商業務 (Sales Rep)** | |

---

## 3. 🤝 共同參與的專案與協作 (Shared Projects & Tasks)

```dataview
TABLE deadline AS "專案截止日", status AS "專案狀態"
FROM "10_Projects"
WHERE contains(file.outlinks, this.file.link) OR contains(file.text, "<% tp.file.title %>")
SORT deadline ASC
```

---

## 4. 📅 歷史會議與交互記錄 (Interaction History)

```dataview
TABLE date AS "會議日期", project AS "所屬專案", type AS "類型"
FROM "20_Areas" OR "10_Projects"
WHERE contains(attendees, "<% tp.file.title %>") OR contains(file.outlinks, this.file.link)
SORT file.name DESC
LIMIT 10
```

---

## 5. 📝 待跟進事項與行動清單 (Open Action Items & Follow-ups)

- [ ] 📌 **最新待辦事項**： (預定跟進日: `next_followup`)
- [ ] 

---

## 6. 📚 相關沉澱資料與技術文檔 (Shared Resources)
- `[[相關文獻筆記或規格書]]`
- `[[相關架構決策或會議筆記]]`
