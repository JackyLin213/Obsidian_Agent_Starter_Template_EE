---
title: "<% tp.file.title %>"
type: area
status: active
tags:
  - Area
  - Area/<% tp.file.title.replace(/\s+/g, '_') %>
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
review_cycle: "每月" # 每週 | 每月 | 每季
owner: "Jacky"
health_status: "🟢 正常" # 🟢 正常 | 🟡 需關注 | 🔴 警示
aliases: []
sources: []
up: "[[20_Areas/Areas_Index]]"
---

# 🛡️ <% tp.file.title %> 責任領域管理

> [!ABSTRACT] 🛡️ 領域概覽與健康度看板 (Area Dashboard)
> - 🎯 **核心使命**：
> - 📏 **維護標準 (SLA)**：
> - 👤 **負責人**：`owner` | **覆盤週期**：`review_cycle`
> - 🚦 **當前健康狀態**：`health_status`
> - 📌 **所屬樞紐**：`up`

---

## 1. 🎯 核心使命與邊界定義 (Mission & Scope)

### 1.1 責任範疇定義 (Scope & Boundaries)
- **核心職責**：
- **邊界與非目標 (Out of Scope)**：
- **長期願景與期望狀態**：

### 1.2 核心原則與價值觀 (Principles & Golden Rules)
1. 
2. 
3. 

---

## 2. 📊 關鍵衡量指標與 SLA 標準 (KPIs & Standards)

| 指標名稱 (Metric) | 基準目標 (Target / SLA) | 目前數值 (Current) | 評估頻率 | 狀態判定 | 備註說明 |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **主要標準 1** | | | 每週 | 🟢 達標 | |
| **主要標準 2** | | | 每月 | 🟢 達標 | |
| **底線標準 (Minimum Bar)** | | | 持續 | 🟢 達標 | 嚴禁低於底線要求 |

---

## 3. 🔄 常態作業流程與例行檢核 (SOPs & Recurring Routines)

### 3.1 週期性例行清單 (Recurring Checklist)
- [ ] 📅 **每日例行 (Daily)**：
- [ ] 🗓️ **每週例行 (Weekly)**：
- [ ] 🌕 **每月例行 (Monthly)**：

### 3.2 領域標準作業程序 (Standard Operating Procedures)
- `[[SOP - 作業流程名稱 1]]`
- `[[SOP - 作業流程名稱 2]]`

---

## 4. 🚀 本領域進行中專案 (Active Projects)

```dataview
TABLE deadline AS "截止日", status AS "專案狀態", file.mtime AS "最後更新"
FROM "10_Projects"
WHERE (contains(area, "<% tp.file.title %>") OR contains(file.tags, "<% tp.file.title %>")) AND status = "active"
SORT deadline ASC
```

---

## 5. 📅 本領域專屬日誌與活動紀錄 (Area Logs & Records)

```dataview
TABLE file.ctime AS "建立日期", tags AS "標籤"
FROM "20_Areas/<% tp.file.title %>/日誌" OR "20_Areas/日誌"
WHERE contains(tags, "<% tp.file.title %>") OR contains(file.tags, "Area/<% tp.file.title %>")
SORT file.name DESC
LIMIT 10
```

---

## 6. 📚 沉澱知識、資源與主題地圖 (Resources & MOCs)

```dataview
LIST file.folder
FROM "30_Resources"
WHERE contains(file.tags, "<% tp.file.title %>") OR contains(tags, "Area/<% tp.file.title %>")
SORT file.mtime DESC
LIMIT 10
```

- 🗺️ **關聯主題地圖 (MOCs)**：`[[MOC - 關聯主題]]`
- 💎 **關鍵永久概念**：`[[關鍵永久筆記]]`
- 📖 **核心文獻與規範**：`[[@關鍵參考資料]]`

---

## 7. 🔄 領域覆盤與持續改進紀錄 (Area Retrospective & Audit)

> 配合 `review_cycle` 定期檢視本領域健康度與流程優化：

- 🏆 **近期重大改善成效**：
- ⚠️ **潛在風險與流程卡點**：
- 🛠️ **下一階段優化行動 (Action Items)**：
  - [ ] 
