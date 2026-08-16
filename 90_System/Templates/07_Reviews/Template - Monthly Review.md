---
title: "<% tp.file.title %>"
type: area
status: active
tags:
  - Review/Monthly
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
monthly_score: 88 # 0-100
review_status: "completed" # in_progress | completed
aliases: []
sources: []
up: "[[20_Areas/日誌]]"
---

# 🌕 <% tp.file.title %> 月度規劃與戰略覆盤

> [!NAV] 快速導航與週期脈絡
> ◀️ [[<% tp.date.now("YYYY-MM", "P-1M", tp.file.title, "YYYY-MM") %>|上個月月報]] | 🗓️ [[<% tp.date.now("YYYY-[Q]Q", 0, tp.file.title, "YYYY-MM") %>|所屬季度]] | ▶️ [[<% tp.date.now("YYYY-MM", "P+1M", tp.file.title, "YYYY-MM") %>|下個月月報]]

---

> [!ABSTRACT] 🌕 月度戰略總覽 (Executive Summary / 30s Scannability)
> - 🎯 **本月主題 (Monthly Theme)**：
> - 🏆 **月度綜合達成評分**：`monthly_score` / 100 | **狀態**：`review_status`
> - 🚀 **專案里程碑交付**：已達成 $\quad$ 個里程碑 / 結案 $\quad$ 個專案
> - 💎 **知識資本沉澱**：本月永久筆記新增 $\quad$ 篇，MOC 新增/更新 $\quad$ 個
> - 🎡 **生活與責任領域平衡指數**： $\quad / 5.0$

---

## 1. 🎯 本月主題與 OKR 達成檢視 (Monthly OKR Review)

### 1.1 戰略任務優先級四象限 (Impact vs Effort Matrix)
```mermaid
quadrantChart
    title 下月戰略任務優先級矩陣 (Impact vs Effort)
    x-axis 低精力投入 --> 高精力投入
    y-axis 低戰略價值 --> 高戰略價值
    quadrant-1 🎯 核心戰略焦點 (Must-Do)
    quadrant-2 ⚡ 快速見效勝利 (Quick Wins)
    quadrant-3 📦 授權或填補 (Delegate)
    quadrant-4 ⚠️ 重新評估效益 (Rethink)
    "主板 EVT 打樣驗證": [0.8, 0.95]
    "SI/PI 仿真工具鏈自動化": [0.4, 0.85]
    "實驗室儀器年度校準": [0.2, 0.7]
```

### 1.2 OKR 目標達成對照表 (Objectives & Key Results)
> [!TARGET] 目標與關鍵結果 (Objectives & Key Results)

| 目標 (Objective) | 關鍵結果 (Key Results) | 基準目標 (Target) | 實際達成 (Actual) | 達成率 (%) | 評分 (0-1.0) |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **O1: ** | **KR 1.1**： | | | | |
| | **KR 1.2**： | | | | |
| **O2: ** | **KR 2.1**： | | | | |
| | **KR 2.2**： | | | | |
| **O3: ** | **KR 3.1**： | | | | |

---

## 2. 🎡 責任領域與生活平衡輪檢視 (Life & Areas Health Check)

| 責任領域 (Area) | 評分 (1-5) | 本月現況與進展摘要 | 下月重點維護策略 |
| :--- | :---: | :--- | :--- |
| 🔬 **硬體技術與研發實力** | | | |
| 🚀 **專案管理與交付品質** | | | |
| 🛠️ **實驗室與儀器資產** | | | |
| 🏃‍♂️ **健康、體能與作息** | | | |
| 💰 **財務與資產配置** | | | |
| 👥 **人際人脈與供應商關係** | | | |
| 🧘‍♂️ **個人成長與心智模型** | | | |

---

## 3. 🚀 本月專案里程碑與結案盤點 (Projects & Deliveries)

```dataview
TABLE deadline AS "截止日", completed_date AS "完成日", status AS "狀態"
FROM "10_Projects" OR "40_Archives/Projects"
WHERE contains(file.mtime, "<% tp.file.title %>") OR status = "completed"
SORT deadline DESC
LIMIT 10
```

---

## 4. 💎 核心知識資本與資產沉澱 (Knowledge Capital Rollup)

> [!NOTE] 💡 本月沉澱之永久卡片與主題地圖

```dataview
TABLE file.ctime AS "沉澱日期", tags AS "標籤"
FROM "30_Resources/02_Permanent" OR "30_Resources/03_MOCs"
WHERE contains(file.cday, "<% tp.file.title %>")
SORT file.ctime DESC
LIMIT 10
```

---

## 5. 🏁 月度深度覆盤與根本反思 (Deep Retrospective)

### 5.1 🌟 值得慶祝的成就與高光時刻 (Highs & Key Wins)
- 

### 5.2 ⚠️ 未達預期目標與根因分析 (Lows & Root Causes)
- **落後項目**：
- **5-Whys 深度根因分析**：
- **組織/個人流程改善對策**：

### 5.3 💎 本月重大洞察與心智模型升級 (Key Insights & Principles)
- 

---

## 6. 🔭 下月戰略定位與三大目標 (Next Month Big Rocks & OKRs)

- **下月核心戰略主題**：
1. 🎯 **下月大石塊 1**：
2. 🎯 **下月大石塊 2**：
3. 🎯 **下月大石塊 3**：
