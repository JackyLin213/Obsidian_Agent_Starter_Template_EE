---
title: "MOC - <% tp.file.title.replace('MOC - ', '') %>"
type: moc
status: evergreen
tags:
  - MOC
  - Hardware/<% tp.file.title.replace('MOC - ', '') %>
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
aliases:
  - "<% tp.file.title.replace('MOC - ', '') %> 知識地圖"
  - "<% tp.file.title.replace('MOC - ', '') %> MOC"
sources: []
up: "[[30_Resources/03_MOCs/MOC - 硬體系統工程總索引]]"
---

# 🗺️ MOC - <% tp.file.title.replace('MOC - ', '') %>

> [!SUMMARY] 🧭 主題全景與知識邊界 (Domain Scope & Overview)
> **領域範疇**：簡述本主題涵蓋之核心物理機制、電路拓撲或工程方法論。  
> **核心標準**：相關行業標準（如 IEEE, JEDEC, IPC-2221, USB-IF, PCIe Base Spec）。  
> **關鍵目標**：本主題旨在解決的系統級工程挑戰（如：電源完整性、阻抗匹配、散熱極限、成本最佳化）。  
> **上層索引**：`up`

---

## 📊 領域知識架構圖 (Knowledge Topology & Mindmap)

```mermaid
mindmap
  root((🗺️ <% tp.file.title.replace('MOC - ', '') %>))
    1. 基礎理論與物理機制
      核心公式推導
      物理邊界條件
    2. 設計規範與佈線準則
      PCB 疊構與 Constraints
      回流路徑與過孔伴隨
    3. 關鍵晶片與選型庫
      主控與週邊 Datasheet
      第二料源與降額清單
    4. 除錯案例與實驗驗證
      5-Whys 根因分析
      ECO 改版驗證記錄
```

---

## 🏛️ 結構化知識導航大綱 (Curated Outline)

### 1. 核心原理與理論公式 (Theoretical Foundations)
*深入底層物理機制，涵蓋傳輸線效應、Maxwell 方程應用、降額準則與計算卡片。*
- [[概念名稱1]] - 核心概念簡述與關鍵公式
- [[概念名稱2]] - 機制原理解析與推導

### 2. 設計實務與佈線準則 (Design Rules & Guidelines)
*電路設計規則、原理圖檢核要點、PCB 疊構與 Layout 規範。*
- [[規範名稱1]] - 回流路徑與過孔配置標準
- [[規範名稱2]] - 去耦電容佈局與開關迴路最小化準則

### 3. 元件規格與選型資料庫 (Components & IC Database)
*關鍵 IC、MOSFET、無源元件之評估規格卡與選型矩陣。*
- [[晶片型號1]] - 封裝、耐壓降額與規格摘要
- [[晶片型號2]] - 主力選型與 Second-Source 替代方案

### 4. 實驗室除錯與踩坑案例 (Debug Case Studies)
*實際硬體 Bring-up、EMI 噪訊、紋波超標之排查與 5-Whys 案例。*
- [[除錯案例1]] - 故障現象、根本原因與臨時 Workaround
- [[除錯案例2]] - 改版 ECO 解決方案與長青沉澱

---

## 🚀 進行中相關專案 (Active Projects)

```dataview
TABLE 
    stage AS "階段",
    health AS "健康度",
    deadline AS "里程碑交付日",
    lead AS "負責人"
FROM "10_Projects"
WHERE contains(file.tags, "<% tp.file.title.replace('MOC - ', '') %>") OR contains(tags, "<% tp.file.title.replace('MOC - ', '') %>")
WHERE status = "active"
SORT deadline ASC
```

---

## 🔬 實戰除錯與排查案例 (Debug & Failure Analysis)

```dataview
TABLE 
    severity AS "嚴重度",
    issue_type AS "問題類型",
    board_rev AS "版本",
    eco_number AS "ECO 編號",
    status AS "狀態"
FROM "30_Resources/02_Permanent"
WHERE contains(tags, "Hardware/Debug") AND (contains(tags, "<% tp.file.title.replace('MOC - ', '') %>") OR contains(file.tags, "<% tp.file.title.replace('MOC - ', '') %>"))
SORT file.mtime DESC
LIMIT 10
```

---

## 💎 長青原子概念卡片 (Permanent Notes)

```dataview
TABLE 
    aliases AS "別名",
    tags AS "標籤",
    file.mtime AS "最後更新"
FROM "30_Resources/02_Permanent"
WHERE (contains(tags, "<% tp.file.title.replace('MOC - ', '') %>") OR contains(file.tags, "<% tp.file.title.replace('MOC - ', '') %>")) AND !contains(tags, "Hardware/Debug")
SORT file.name ASC
```

---

## 📖 原廠文獻與技術白皮書 (Literature & App Notes)

```dataview
TABLE 
    author AS "原廠/作者",
    publication_year AS "年份",
    rating AS "評分",
    file.folder AS "存放目錄"
FROM "30_Resources/01_Literature"
WHERE contains(tags, "<% tp.file.title.replace('MOC - ', '') %>") OR contains(file.tags, "<% tp.file.title.replace('MOC - ', '') %>")
SORT file.ctime DESC
LIMIT 10
```

---

## 📥 待清洗與未分類筆記 (Inbox / Drafts)

```dataview
TABLE 
    file.folder AS "目錄",
    file.ctime AS "建立日期"
FROM "00_Inbox" OR "30_Resources"
WHERE (contains(tags, "<% tp.file.title.replace('MOC - ', '') %>") OR contains(file.tags, "<% tp.file.title.replace('MOC - ', '') %>")) AND (status = "inbox" OR status = "draft")
SORT file.ctime DESC
```
