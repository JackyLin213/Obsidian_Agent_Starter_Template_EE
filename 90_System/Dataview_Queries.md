# 常用 Dataview 查詢代碼庫 (Dataview Queries Library)

本文件整理了知識庫中常用的 Dataview 與 DataviewJS 查詢語法，可直接複製至 MOC、個人儀表板（Dashboard）或硬體工程專題筆記中使用。

---

## 1. 收集箱待處理清單 (Inbox Triage)
列出 `00_Inbox` 中尚未清洗提煉的草稿筆記：

```dataview
TABLE file.ctime AS "建立時間", tags AS "標籤"
FROM "00_Inbox"
WHERE status = "inbox" OR status = "draft"
SORT file.ctime DESC
```

---

## 2. 進行中的專案 (Active Projects Dashboard)
列出目前正在進行中的專案與其截止日期、所屬責任領域：

```dataview
TABLE deadline AS "截止日", area AS "責任領域", file.mtime AS "最後更新"
FROM "10_Projects"
WHERE status = "active"
SORT deadline ASC
```

---

## 3. 🚨 硬體除錯與實驗問題看板 (Hardware Debug Tracker)
列出所有尚未解決或已完成驗證的硬體 Issue（按嚴重程度與版本排序）：

```dataview
TABLE project AS "所屬專案", board_rev AS "版本", board_sn AS "板號", severity AS "嚴重度", issue_type AS "領域", eco_number AS "ECO單號", status AS "除錯狀態"
FROM "30_Resources" OR "10_Projects"
WHERE contains(tags, "Hardware/Debug") AND status != "closed"
SORT severity ASC, file.mtime DESC
```

### 查詢特定專案已發布 ECO 待下一版本驗證的 Issue：
```dataview
TABLE eco_number AS "ECO單號", board_rev AS "當前版本", issue_type AS "領域", status AS "狀態"
FROM "30_Resources" OR "10_Projects"
WHERE contains(tags, "Hardware/Debug") AND (status = "resolved_in_eco" OR status = "workaround_verified")
SORT file.mtime DESC
```

---

## 4. ⚡ 晶片與元器件選型資料庫 (IC & Component Catalog)
依類別與原廠列出知識庫中已沉澱的元器件資料庫：

```dataview
TABLE manufacturer AS "原廠", category AS "類別", package AS "封裝", temp_grade AS "溫度等級", second_source_status AS "第二料源", lifecycle_status AS "生命週期", unit_price_usd AS "單價"
FROM "30_Resources"
WHERE contains(tags, "Hardware/Component")
SORT category ASC, manufacturer ASC
```

### 查詢單一料源或高供應鏈風險元器件清單 (Single Source Risk Tracker)：
```dataview
TABLE manufacturer AS "原廠", package AS "封裝", lead_time_weeks AS "交期(週)", lifecycle_status AS "生命週期"
FROM "30_Resources"
WHERE contains(tags, "Hardware/Component") AND (contains(second_source_status, "Single Source") OR lifecycle_status = "NRND" OR lifecycle_status = "EOL")
SORT file.mtime DESC
```

---

## 5. 🌊 訊號與電源完整性知識庫 (SI/PI & PCB Design Index)
列出所有關於 SI/PI、傳輸線、PDN、去耦與疊構的長青永久卡片：

```dataview
TABLE aliases AS "別名", up AS "所屬 MOC", file.mtime AS "最後更新"
FROM "30_Resources/02_Permanent"
WHERE (contains(tags, "SIPI") OR contains(tags, "PCB") OR contains(tags, "Power") OR contains(tags, "Hardware")) AND status = "evergreen"
SORT file.name ASC
```

---

## 6. 📚 原廠應用手冊與標準規範 (Hardware App Notes & Standards)
追蹤已清洗的 TI, ADI, MPS 應用筆記與 PCIe/DDR/USB 規範標準：

```dataview
TABLE author AS "原廠/作者", year AS "年份", rating AS "推薦度", sources AS "出處"
FROM "30_Resources/01_Literature"
WHERE contains(tags, "Literature") AND (contains(tags, "Hardware") OR contains(tags, "AppNote") OR contains(tags, "Standard"))
SORT file.ctime DESC
```

---

## 7. 架構決策與決策日誌 (Decision Records / ADRs)
列出所有已採納的硬體/軟體架構決策及其覆盤時間：

```dataview
TABLE decision_date AS "決策日", status AS "狀態", review_date AS "預定覆盤日", project AS "關聯專案"
FROM "30_Resources" OR "10_Projects"
WHERE contains(tags, "Decision/ADR")
SORT review_date ASC
```

---

## 8. 會議記錄追蹤 (Meetings by Project / Person)
### 查詢特定專案的所有歷史會議：
```dataview
TABLE date AS "日期", attendees AS "參與者", location AS "地點"
FROM "20_Areas" OR "10_Projects"
WHERE contains(tags, "Meeting") AND contains(project, "專案名稱")
SORT date DESC
```

---

## 9. 人脈 CRM (Personal CRM Contact Tracker)
列出需要定期維護的人脈與上次聯絡時間：

```dataview
TABLE company AS "公司", role AS "職稱", contact_frequency AS "聯絡頻率", last_contacted AS "上次聯絡"
FROM "20_Areas"
WHERE contains(tags, "People/Contact")
SORT last_contacted ASC
```

---

## 10. 最近 7 天的每日覆盤 (Recent Daily Notes)
```dataview
TABLE file.day AS "日期"
FROM "20_Areas/日誌"
SORT file.name DESC
LIMIT 7
```

---

## 11. 🐞 軟體故障與事故排查看板 (Software Bug & Incident Tracker)
列出所有未結案的軟體 Bug 與生產事故（按嚴重度與更新時間排序）：

```dataview
TABLE project AS "專案", severity AS "嚴重度", category AS "分類", affected_version AS "影響版本", assignee AS "負責人", status AS "狀態"
FROM "30_Resources/02_Permanent" OR "10_Projects"
WHERE contains(tags, "Software/Bug") AND status != "closed"
SORT severity ASC, file.mtime DESC
```

---

## 12. 🌐 API 介面與服務契約目錄 (API & Services Catalog)
依傳輸協議與方法列出知識庫中定義的 API 介面清單：

```dataview
TABLE method AS "方法", api_path AS "端點路徑", protocol AS "協議", rate_limit AS "流控", service_owner AS "負責人", status AS "狀態"
FROM "30_Resources/02_Permanent"
WHERE contains(tags, "Software/API")
SORT api_path ASC
```

---

## 13. 🏛️ 軟體架構 RFC 提案管道 (Software RFC Pipeline)
追蹤所有架構重構提案與技術規格審查進度：

```dataview
TABLE rfc_number AS "RFC單號", target_release AS "目標版本", authors AS "作者", status AS "狀態", file.mtime AS "最後更新"
FROM "30_Resources/02_Permanent"
WHERE contains(tags, "Software/RFC")
SORT rfc_number DESC
```

---

## 14. ⚡ 嵌入式驅動與韌體模組庫 (Firmware & Driver Registry)
列出已封裝的 MCU / RTOS 晶片驅動與硬體抽象層 (HAL)：

```dataview
TABLE target_chip AS "目標晶片", bus_type AS "匯流排", bus_clock_speed AS "速率", os_target AS "OS環境", status AS "狀態"
FROM "30_Resources/02_Permanent"
WHERE contains(tags, "Software/Embedded") OR contains(tags, "Hardware/Firmware")
SORT file.name ASC
```

---

## 15. 💻 演算法與常用程式碼模式庫 (Code Snippets & Patterns)
依語言與模式類型檢索高效能原子代碼片段：

```dataview
TABLE language AS "語言", pattern_type AS "模式類型", time_complexity AS "時間複雜度", thread_safe AS "執行緒安全"
FROM "30_Resources/02_Permanent"
WHERE contains(tags, "Software/Pattern") OR contains(tags, "Software/Snippet")
SORT language ASC, pattern_type ASC
```

---

## 16. 🔄 韌體 RTOS 任務架構與系統狀態看板 (Firmware Architecture & RTOS Registry)
列出所有已規劃的 MCU 平台與 RTOS 任務架構：

```dataview
TABLE target_mcu AS "目標 MCU", rtos_kernel AS "RTOS 核心", tick_rate_hz AS "Tick", system_clock_mhz AS "主頻", lead_architect AS "架構師"
FROM "30_Resources/02_Permanent"
WHERE contains(tags, "Firmware/RTOS") OR contains(tags, "Firmware/Architecture")
SORT file.name ASC
```

---

## 17. 📦 韌體通訊協議與封包幀目錄 (Firmware Protocols & Packets Catalog)
依實體層與封包格式檢索自訂通訊協議清單：

```dataview
TABLE physical_layer AS "實體層", frame_encoding AS "幀編碼", checksum_type AS "校驗", max_payload_size AS "最大載荷", project AS "專案"
FROM "30_Resources/02_Permanent"
WHERE contains(tags, "Firmware/Protocol")
SORT file.name ASC
```

---

## 18. 🛡️ 韌體 Bootloader 與 OTA 升級規格清單 (Bootloader & OTA Specs Tracker)
追蹤板卡引導載入與 OTA 安全升級規格：

```dataview
TABLE target_mcu AS "目標 MCU", ota_strategy AS "升級策略", signature_algorithm AS "簽名演算法", anti_rollback_version AS "防回滾版本"
FROM "30_Resources/02_Permanent"
WHERE contains(tags, "Firmware/OTA") OR contains(tags, "Firmware/Bootloader")
SORT file.name ASC
```
