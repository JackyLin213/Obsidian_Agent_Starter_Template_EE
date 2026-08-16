---
title: "<% tp.file.title %>"
type: area
status: active
tags:
  - Review/Weekly
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
weekly_score: 85 # 0-100
review_status: "completed" # in_progress | completed
aliases: []
sources: []
up: "[[20_Areas/日誌]]"
---

# 📊 <% tp.file.title %> 週度覆盤與戰略規劃

> [!NAV] 快速導航與週期脈絡
> ◀️ [[<% tp.date.now("gggg-[W]ww", -7, tp.file.title, "gggg-[W]ww") %>|上一週週報]] | 🌕 [[<% tp.date.now("YYYY-MM", 0, tp.file.title, "gggg-[W]ww") %>|所屬月份月報]] | 🗓️ [[<% tp.date.now("YYYY-[Q]Q", 0, tp.file.title, "gggg-[W]ww") %>|所屬季度]] | ▶️ [[<% tp.date.now("gggg-[W]ww", 7, tp.file.title, "gggg-[W]ww") %>|下一週週報]]

---

> [!ABSTRACT] 📊 本週戰情報告 (Weekly Scorecard / 30s Scannability)
> - 🏆 **週度綜合得分**：`weekly_score` / 100 | **覆盤狀態**：`review_status`
> - 🎯 **大石塊達成率**： $\quad / 3$ (完成率: $\quad \%$)
> - 🚦 **專案交付健康度**：🟢 正常 / 🟡 需注意 / 🔴 延遲風險
> - 🔬 **硬體除錯與 ECO 進展**：本週新提 $\quad$ 件，已閉環 $\quad$ 件

---

## 1. 🎯 本週三大核心焦點覆盤 (Weekly Big Rocks Review)

1. [ ] 🌟 **大石塊 1**： 
   - *結果與進展*：
2. [ ] 🌟 **大石塊 2**： 
   - *結果與進展*：
3. [ ] 🌟 **大石塊 3**： 
   - *結果與進展*：

---

## 2. 🚀 專案交付健康度與里程碑檢核 (Active Projects & Milestones)

```dataview
TABLE deadline AS "截止日", status AS "狀態", file.mtime AS "最後更新"
FROM "10_Projects"
WHERE status = "active"
SORT deadline ASC
```

---

## 3. 🔬 硬體 Issue 與除錯進展看板 (Hardware Debug & ECO Rollup)

> [!TIP] 💡 本週聚焦之硬體除錯與 ECO 變更紀錄

```dataview
TABLE severity AS "嚴重度", issue_type AS "領域", board_rev AS "版本", status AS "狀態"
FROM "30_Resources/02_Permanent/Hardware/Debug"
WHERE file.mtime >= date("<% tp.date.now('YYYY-MM-DD', -7, tp.file.title, 'gggg-[W]ww') %>")
SORT severity ASC, file.mtime DESC
```

---

## 4. 📝 當週日誌回顧與靈感聚合 (Daily Notes Rollup)

```dataview
TABLE file.ctime AS "建立時間", energy_level AS "精力", focus_score AS "專注度"
FROM "20_Areas/日誌"
WHERE file.day >= date("<% tp.date.now('YYYY-MM-DD', -6, tp.file.title, 'gggg-[W]ww') %>") AND file.day <= date("<% tp.date.now('YYYY-MM-DD', 0, tp.file.title, 'gggg-[W]ww') %>")
SORT file.name ASC
```

---

## 5. 📥 知識庫維護與 Inbox Zero 審計 (Vault & Pipeline Audit)

- [ ] **收集箱清洗 (Inbox Zero)**：已將 `00_Inbox/` 中已處理資料移至 `40_Archives/Inbox_History/`
- [ ] **文獻筆記提煉**：本週新增 $\quad$ 篇 `@文獻筆記`
- [ ] **永久原子卡片沉澱**：本週新增 $\quad$ 篇 `02_Permanent/Hardware/` 卡片
- [ ] **主題地圖 (MOC) 更新**：相關 MOC 已同步最新連結

---

## 6. 🏁 週度深度覆盤反思 (Weekly Retrospective)

### 6.1 🏆 重大成果與高光亮點 (Wins & Highlights)
- 

### 6.2 🚧 阻礙、卡點與根本原因 (Blockers & Root Cause Analysis)
- **卡點現象**：
- **5-Whys 簡要根因**：
- **改進對策 (ECO / Action Plan)**：

### 6.3 💡 流程或設計優化點 (Kaizen / Process Improvements)
- 

---

## 7. 🔭 下週核心戰略與三大焦點 (Next Week Big Rocks)

1. [ ] 🎯 **下週大石塊 1 (MIT 1)**：
2. [ ] 🎯 **下週大石塊 2 (MIT 2)**：
3. [ ] 🎯 **下週大石塊 3 (MIT 3)**：
