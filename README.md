# Obsidian AI 知識庫啟動模板 (Obsidian Agent Starter Template)

> **版本**：v5.0.0 (Tri-Stack Systems Edition: EE × FW × SW)  
> **體系**：PARA (Projects, Areas, Resources, Archives) × Zettelkasten (卡片盒筆記法) 深度融合  
> **定位**：專為**全棧系統架構師 (Tri-Stack Systems Architect: Hardware × Firmware × Software)** 打造之數位第二大腦與工程管理規範

歡迎使用結合 **PARA 方法論**、**Zettelkasten 卡片盒筆記法**、**Templater JS 動態自動化** 與 **AI Agent 協同架構** 的現代化 Obsidian 第二大腦！

本專案深度客製化支援 **硬體工程 (EE)**、**嵌入式韌體 (FW)** 與 **現代軟體工程 (SW)** 的三位一體全棧研發生命週期，內建對 **SI/PI**、**PCB 疊構**、**電源拓撲**、**晶片選型**、**硬體除錯**、**RTOS 任務排程**、**通訊協議封包**、**Bootloader/OTA**、**軟體 Crash 事故覆盤**、**API 契約**、**技術 RFC** 與 **演算法代碼模式** 的全流程工程管理。

---

## 🌟 核心特色

- 🔬 **硬體系統工程套件 (EE Suite)**：內建 `Hardware Debug Note`（波形截圖、5-Whys 根因分析、飛線改板與 ECO）與 `Component Spec`（75%/60% 降額檢核、Layout 避坑、第二料源）。
- ⚡ **嵌入式韌體工程套件 (FW Suite)**：內建 `Firmware Driver Spec`（暫存器映射、I2C/SPI 時序）、`Firmware Architecture & RTOS Spec`（FSM 狀態機、任務優先級、堆疊預算、多任務看門狗）、`Firmware Protocol & Packet Spec`（二進位幀格式、TLV/命令集、CRC、重傳機制）與 `Firmware Bootloader & OTA Spec`（Flash 分區地圖、A/B 雙分區熱切換、ECDSA 簽名防回滾）。
- 💻 **軟體系統工程套件 (SW Suite)**：內建 `Software Bug Note`（Call Stack 堆疊、MRE 重現、CI 回歸防線）、`API Spec`（REST/gRPC 介面契約、時序圖）、`Software RFC`（架構提案、SQL 資料模型、灰度遷移）與 `Code Snippet / Pattern`（複雜度分析、Cache 對齊）。
- 🏛️ **PARA × Zettelkasten 頂級融合**：以 PARA 驅動研發專案 (EVT/DVT/PVT 或 Release vX.Y) 與責任領域，以卡片盒沉澱跨領域長青原子知識。
- 🤖 **AI Agent 雙軌整理流水線 (`AGENTS.md` v5.0.0)**：內建「單筆 5 步提煉狀態機」與「全庫 5 大防禦巡檢矩陣」，支援自動防重檢索、MOC 主動織網自愈、Inbox Zero 歸檔與操作安全分級。
- 📑 **全套 25 大場景專業模板 (7 大模組化目錄)**：依工程職責嚴格分類為硬體、韌體、軟體、知識、專案、實體與覆盤 7 大子目錄。
- 📊 **多維視覺繪圖規範 (Diagramming Standards)**：內建 11 大研發場景圖表選型矩陣（Mermaid `flowchart`, `stateDiagram`, `sequenceDiagram`, `gantt`, `mindmap`, `erDiagram`, `quadrantChart` + `WaveDrom` 數位匯流排時序 + `ASCII Box` 記憶體地圖/引腳佈局 + 原生 Canvas 畫布）。
- 📊 **Dataview 動態看板**：提供開箱即用的軟硬韌 Issue 看板、元件庫查詢、RTOS 任務清單、協議目錄、API 目錄、RFC 管道與專案追蹤。

---

## 📁 目錄結構說明

```
.
├── 00_Inbox/                  # [收集箱] 靈感、隨手問題、待清洗剪藏的暫存入口
│   └── Clippings/             # [剪藏暫存] 網頁剪藏、晶片 App Note 與 API 規格預設存入區（自動納管）
├── 10_Projects/               # [專案] 具明確目標與截止日的研發專案（<YYYY-專案名稱_階段>.md）
├── 20_Areas/                  # [領域] 長期維護的責任範疇（硬體實驗室、軟體基礎設施等）
│   ├── 日誌/                  # [全域日誌與覆盤] 每日日誌 (YYYY-MM-DD.md)、週報 (YYYY-Www.md)、月報 (YYYY-MM.md)
│   └── <責任領域名稱>/         # 特定領域管理目標與專業日誌
├── 30_Resources/              # [知識庫核心 - Zettelkasten 沉澱區]
│   ├── 01_Literature/         # 文獻筆記：晶片 App Notes、論文摘要、白皮書、書籍精讀（@作者_標題.md）
│   ├── 02_Permanent/          # 原子永久筆記：SI/PI 理論、韌體架構、軟體演算法、除錯記錄（至多 3 階子資料夾）
│   │   ├── Hardware/          # [硬體專題沉澱] SIPI/, Power/, PCB/, Components/, Debug/
│   │   ├── Firmware/          # [韌體專題沉澱] Drivers/, RTOS/, Protocols/, OTA/
│   │   └── Software/          # [軟體專題沉澱] Bug/, API/, RFC/, Embedded/, Patterns/
│   └── 03_MOCs/               # 主題地圖 (Maps of Content)：領域知識樞紐（MOC - 主題.md）
├── 40_Archives/               # [歸檔] 歷史封存檔案
│   ├── Projects/              # 已結案封存的歷史專案 (EVT/DVT/PVT 結案或軟體版本封存)
│   └── Inbox_History/         # 已提煉完成之 Inbox 歷史原始檔（Inbox Zero 封存）
└── 90_System/                 # [系統設定] 模板庫、附件與 Dataview 語法參考
    ├── Attachments/           # 附件集中存放區（示波器波形圖、PCB 圖紙、架構圖、PDF 等）
    ├── Dataview_Queries.md    # 常用 Dataview 查詢代碼庫 (含軟硬韌 Issue 看板、API 目錄與元件庫)
    └── Templates/             # 25 大標準筆記模板庫 (分 7 大模組化子資料夾)
        ├── 01_Hardware/       # 🔬 [硬體工程 2 款] (Debug, Component)
        ├── 02_Firmware/       # ⚡ [嵌入式韌體 4 款] (Driver, RTOS, Protocol, OTA)
        ├── 03_Software/       # 💻 [軟體工程 4 款] (Bug, API, RFC, Pattern)
        ├── 04_Knowledge/      # 💎 [知識沉澱 6 款] (Permanent, Literature, Book, Paper, Fleeting, MOC)
        ├── 05_Projects/       # 🎯 [專案與執行 4 款] (Project, Meeting, Decision, Area)
        ├── 06_Entities/       # 👤 [實體與資源 2 款] (Person, Tool/Resource)
        └── 07_Reviews/        # 📅 [週期覆盤 3 款] (Daily, Weekly, Monthly)
```

---

## 📚 25 大核心模板清單 (`90_System/Templates/`)

| 子資料夾 | 模板名稱 | 適用場景與特色 |
| :--- | :--- | :--- |
| **`01_Hardware/`** | `Template - Hardware Debug Note.md` ⭐ | **硬體除錯/測試實驗**：量測波形截圖、5-Whys 根因分析、飛線改板與 ECO 閉環 |
| | `Template - Component Spec.md` ⭐ | **晶片/元件選型**：電氣參數表、75%/60% 降額檢核、Vendor Layout 避坑、第二料源 |
| **`02_Firmware/`** | `Template - Firmware Driver Spec.md` ⚡ | **晶片驅動/HAL 規格**：暫存器映射、I2C/SPI 時序、HAL API 宣告、硬體防死鎖恢復 |
| | `Template - Firmware Architecture & RTOS Spec.md` ⚡ | **韌體架構/RTOS 規格**：時鐘樹、FSM 狀態機、任務堆疊預算、IPC 同步、多任務看門狗 |
| | `Template - Firmware Protocol & Packet Spec.md` ⚡ | **通訊協議/封包幀規格**：二進位幀格式、TLV/命令集、FSM 解析狀態機、CRC 校驗、重傳機制 |
| | `Template - Firmware Bootloader & OTA Spec.md` ⚡ | **引導載入/OTA 升級**：Flash 分區地圖、A/B 雙分區無縫熱切換、ECDSA 簽名防回滾、防磚機制 |
| **`03_Software/`** | `Template - Software Bug Note.md` 🚀 | **軟體除錯/事故覆盤**：Call Stack 堆疊、MRE 重現、5-Whys、Code Diff、CI 回歸防線 |
| | `Template - API Spec.md` 🚀 | **API/服務介面規格**：REST/gRPC 契約、Request/Response Schema、Mermaid 時序圖 |
| | `Template - Software RFC.md` 🚀 | **架構提案/技術規格**：系統架構圖、SQL 資料模型、HA/安全性評估、Trade-offs 矩陣 |
| | `Template - Code Snippet or Pattern.md` 🚀 | **代碼模式/演算法**：多語言慣用代碼、時間/空間複雜度 $O(N)$、邊界防呆、單元測試 |
| **`04_Knowledge/`** | `Template - Permanent Note.md` | **原子永久筆記**：本質定義+拇指法則雙層導讀、物理/數學/電路機制、DOs/DON'Ts、4D 語意網絡 |
| | `Template - Literature Note.md` | **原廠文獻/App Note**：TI/ADI 應用筆記、設計計算、Layout 避坑、原子蒸餾流 |
| | `Template - Paper Note.md` | **學術研究論文**：IEEE 論文、Research Canvas、量化評估表、工業落地批判 |
| | `Template - Book Note.md` | **出版書籍精讀**：全書 Mermaid 架構心智圖、3大心智模型、Rule of Thumb、落地清單 |
| | `Template - Fleeting Note.md` | **靈感捕捉卡**：閃電捕捉、科學假說 If-Then-Because、快速驗證、分流決策樹 |
| | `Template - MOC.md` | **主題地圖**：領域範疇全景、Mermaid 知識拓撲、4大導航分類、動態 Dataview 看板 |
| **`05_Projects/`** | `Template - Project.md` | **研發專案卡**：EVT/DVT/PVT 階段門檢核、甘特進程圖、硬體設計資產、跨庫追蹤 |
| | `Template - Meeting Note.md` | **會議記錄**：Schematic/Layout Review 評審結論看板 (PASS/FAIL)、技術爭議權衡矩陣 |
| | `Template - Decision Record.md` | **架構決策 (ADR)**：定量方案對比矩陣 (BOM/面積/熱/供應鏈)、V&V 驗收標準、ECO 連動 |
| | `Template - Area Note.md` | **責任領域**：SLA 維護標準、SOP 流程庫、專屬日誌與沉澱資源三重視角 |
| **`06_Entities/`** | `Template - Person.md` | **人脈 CRM**：原廠 FAE/業務對接通道、支援晶片系列、樣品申請、歷史會議追蹤 |
| | `Template - Tool or Resource.md` | **工具與儀器**：AMR 極限額定、ESD/探棒安全量測 SOP、Python SCPI 自動化代碼、校準履歷 |
| **`07_Reviews/`** | `Template - Daily Note.md` | **每日日誌**：跨週期導航、今日吃青蛙 (MIT) 焦點、時間軸隨走隨記、Lab 快記區 |
| | `Template - Weekly Review.md` | **週度覆盤**：週度戰情報告、三大焦點大石塊覆盤、軟硬韌 Issue/ECO 看板、Inbox Zero |
| | `Template - Monthly Review.md` | **月度規劃**：月度戰略總覽、OKR 量化評分表、7 大責任領域平衡輪、永久卡片沉澱 |

---

## 🚀 如何在軟硬韌研發場景與 AI 協同？

### 1. 記錄與排查硬體 Issue (Hardware Debug)
> **你對 Agent 說**：「EVT 板子上的 12V 轉 1.0V VDD_CORE 電源紋波高達 90mVpk-pk 導致當機，實測波形發現 SW 節點有 300MHz 振鈴，幫我建一張 Debug 卡片。」  
> **Agent 會做的事**：自動套用 `01_Hardware/Template - Hardware Debug Note.md`，結構化記錄重現條件、量測數據、5-Whys 假設推導（判定為寄生電感與去耦電容佈局不良），並提供 Snubber 電路計算與 Workaround 記錄。

### 2. 韌體 RTOS 任務規劃與通訊封包設計 (Firmware Architecture & Protocol)
> **你對 Agent 說**：「幫我為 STM32H7 規劃 FreeRTOS 任務架構與堆疊預算，以及設計一組基於 UART 的二進位通訊幀格式與 CRC16 校驗。」  
> **Agent 會做的事**：分別套用 `02_Firmware/Template - Firmware Architecture & RTOS Spec.md`（規劃 5 大任務優先級、FSM 狀態機與多任務看門狗掩碼）與 `02_Firmware/Template - Firmware Protocol & Packet Spec.md`（繪製二進位幀圖、定義命令集與 FSM 解析狀態機）。

### 3. 軟體生產事故與 Crash 排查 (Software Bug)
> **你對 Agent 說**：「在高併發壓力測試下，TCP 連線重置導致 worker 執行緒發生 Segmentation Fault，這是 GDB 堆疊，請幫我建立事故覆盤卡。」  
> **Agent 會做的事**：自動套用 `03_Software/Template - Software Bug Note.md`，解析 Call Stack，進行 5-Whys 競爭根因推導，提供 Mutex 互斥鎖修復代碼對比 (Diff) 與單元測試回歸防線。

### 4. 筆記提煉與知識庫健康巡檢 (Note Distillation & Vault Linting)
> **你對 Agent 說**：「整理 `00_Inbox` 中的這篇原廠 App Note 剪藏，並對整份知識庫執行一次健康檢查。」  
> **Agent 會做的事**：
> 1. 執行 **單筆提煉 5 步狀態機**：防重檢索 ➔ 匹配 `Template - Literature Note.md` ➔ 注入 EE 審查準則與 Frontmatter ➔ 自動寫入 `02_Permanent` 並向上掛載至對應 MOC ➔ 封存 Inbox 原始檔至 `40_Archives/Inbox_History/`。
> 2. 執行 **全庫 5 大防禦巡檢**：掃描全庫斷鏈、孤島筆記、目錄層級違規、Schema 合規與 Mermaid 防爆，產出修復診斷報告。

---

詳細的 Agent 工作流程與規範請參閱 [AGENTS.md](AGENTS.md) 或 `[[AGENTS]]`。

