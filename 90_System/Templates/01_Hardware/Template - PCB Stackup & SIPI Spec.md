---
title: "<% tp.file.title %>"
type: permanent
status: draft # draft | in_review | approved | frozen
tags:
  - Hardware/PCB
  - Hardware/SIPI # Hardware/SIPI | Hardware/Stackup | Hardware/Layout
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
project: "[[10_Projects/專案名稱]]"
board_rev: "EVT" # EVT | DVT | PVT | Rev A
layer_count: 8 # 4 | 6 | 8 | 10 | 12
board_thickness_mm: "1.6mm"
material_type: "IT-180TC (Tg 180°C)" # FR4 (IT-180TC) | Megtron 6 | Rogers 4350B | Shengyi S1000-2M
diff_impedance_target: "90Ω / 100Ω"
single_ended_impedance: "50Ω"
pcb_vendor: "勝宏科技 / 健鼎 / 欣興"
aliases: []
sources: []
up: "[[30_Resources/03_MOCs/MOC - PCB 疊構與高速訊號完整性 (PCB & SIPI)]]"
---

# 📐 <% tp.file.title %> PCB 疊構與 SI/PI 設計規格書

> [!ABSTRACT] ⚡ 30 秒疊構與 PCB 規格速讀 (Stackup Verdict / TL;DR)
> - 🔢 **層數與板厚**：`layer_count` 層板 | 總成品厚度 **`board_thickness_mm`**
> - 🧱 **基材規格**：`material_type` ($D_k \approx 4.1, D_f \approx 0.015\ @\ 1\text{GHz}$)
> - 🌊 **阻抗控制**：單端 **`single_ended_impedance`** | 差分 **`diff_impedance_target`** ($\pm 10\%$ 公差)
> - 🛡️ **回流防禦**：高速信號相鄰完整 Ground Plane，嚴禁跨分割；換層過孔配置伴隨接地過孔 (Stitching Vias)
> - 📋 **所屬專案與狀態**：`project` (`board_rev`) | 板廠：`pcb_vendor` | **審查狀態**：`status`

---

## 1. 📐 PCB 物理規格與疊構結構表 (Layer Stackup & Dielectric Map)

### 1.1 8 層標準對稱疊構詳細結構表 (8-Layer High-Speed Stackup)

| 層號 (Layer) | 層屬性 (Type) | 銅箔厚度 (Copper) | 介質材料 (Dielectric) | 介質厚度 (Thickness) | 介電常數 ($D_k$) | 損耗角正切 ($D_f$) | 參考地平面 (Ref Plane) |
| :---: | :---: | :---: | :--- | :---: | :---: | :---: | :--- |
| **L1 (TOP)** | 🔴 Signal (HS) | 1.0 oz (Finished) | Prepreg 1080 (1x) | $2.8\text{ mil}$ | $3.9$ | $0.016$ | **L2 (GND1)** |
| **L2 (GND1)**| ⚫ Ground Plane | 1.0 oz | Core (IT-180TC) | $4.0\text{ mil}$ | $4.2$ | $0.015$ | -- (完整地屏蔽) |
| **L3 (SIG1)**| 🔴 Signal / Bus | 1.0 oz | Prepreg 2116 (2x) | $8.0\text{ mil}$ | $4.0$ | $0.015$ | **L2 (GND1) / L4 (PWR1)** |
| **L4 (PWR1)**| 🔵 Power Plane | 1.0 oz | Core (Center Core)| $16.0\text{ mil}$| $4.3$ | $0.015$ | -- (主電源平面) |
| **L5 (GND2)**| ⚫ Ground Plane | 1.0 oz | Prepreg 2116 (2x) | $8.0\text{ mil}$ | $4.0$ | $0.015$ | -- (完整地屏蔽) |
| **L6 (SIG2)**| 🔴 Signal (HS) | 1.0 oz | Core (IT-180TC) | $4.0\text{ mil}$ | $4.2$ | $0.015$ | **L5 (GND2)** |
| **L7 (GND3)**| ⚫ Ground Plane | 1.0 oz | Prepreg 1080 (1x) | $2.8\text{ mil}$ | $3.9$ | $0.016$ | -- (次電源/地) |
| **L8 (BOT)** | 🔴 Signal / IO | 1.0 oz (Finished) | -- | -- | -- | -- | **L7 (GND3)** |

### 1.2 物理加工參數與公差控制 (Fabrication Tolerances)
- **總成品板厚 (Finished Board Thickness)**：$1.6\text{ mm} \pm 10\%$ ($63\text{ mil}$)
- **最小走線寬度 / 線距 (Min Trace / Space)**：$3.5\text{ mil} / 3.5\text{ mil}$
- **最小導通孔孔徑 / 焊盤 (Min Via / Pad)**：$0.2\text{ mm} (8\text{ mil}) / 0.4\text{ mm} (16\text{ mil})$
- **表面處理工藝 (Surface Finish)**：化學沉金 ENIG ($2\sim 3\,\mu''\text{ Gold over }150\,\mu''\text{ Nickel}$)
- **防焊漆 (Solder Mask)**：霧面黑 / 綠色，耐溫 $\ge 260^\circ\text{C}$（無鉛回流焊標準）

---

## 2. 🌊 特性阻抗控制模型與約束計算 (Controlled Impedance Spec & Sizing)

### 2.1 阻抗控制矩陣與幾何走線表
| 走線類型 (Transmission Line) | 適用信號類別 | 走線層 (Layer) | 走線寬度 ($W$) | 線間距 ($S$) | 參考平面 | 目標阻抗 ($Z_0 / Z_{diff}$) | 允許公差 |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **單端微帶線 (SE Microstrip)** | Clock, SPI, GPIO | L1, L8 | $4.5\text{ mil}$ | -- | L2, L7 | **$50.0\,\Omega$** | $\pm 10\%$ |
| **單端帶狀線 (SE Stripline)** | High-Speed Single | L3, L6 | $4.0\text{ mil}$ | -- | L2/L4, L5/L7 | **$50.0\,\Omega$** | $\pm 10\%$ |
| **差分微帶線 (Diff Microstrip)**| USB 2.0 (High Speed) | L1, L8 | $5.5\text{ mil}$ | $5.0\text{ mil}$ | L2, L7 | **$90.0\,\Omega$** | $\pm 10\%$ |
| **差分微帶線 (Diff Microstrip)**| PCIe Gen3 / GbE | L1, L8 | $4.8\text{ mil}$ | $4.2\text{ mil}$ | L2, L7 | **$100.0\,\Omega$** | $\pm 10\%$ |
| **差分帶狀線 (Diff Stripline)** | PCIe / DDR Clock | L6 | $4.2\text{ mil}$ | $4.8\text{ mil}$ | L5, L7 | **$100.0\,\Omega$** | $\pm 10\%$ |
| **共面差分波導 (CPW with GND)**| RF 2.4G/5.8G 天線 | L1 | $10.0\text{ mil}$| $6.0\text{ mil}$ | L2 (GND) | **$50.0\,\Omega$** | $\pm 5\%$ |

---

## 3. 🛡️ 訊號完整性 (SI) 回流路徑與過孔防呆 (SI Return Path & Routing Rules)

> [!TIP] 🔬 首席架構師高頻回流鐵律
> 高頻電流依循「**最低阻抗（最小電感）路徑**」回流，即緊貼走線正下方的接地平面。
> 任何跨越平面分割（Cross-Split）的走線都會迫使回流信號繞道，形成巨大天線環路，導致嚴重的 EMI 輻射與信號失真！

### 3.1 換層過孔與接地伴隨孔配置 (Via Transitions & Ground Stitching)
```text
      Signal Via                 Ground Stitching Via (< 20 mil)
         │                                    │
Layer 1  ●═════════ (TOP Trace)               │
         │                                    │
Layer 2 ─── (GND 1) ────[ Anti-pad ]──────────●────────── (GND Plane)
         │                                    │
Layer 3  │                                    │
Layer 4  │                                    │
Layer 5 ─── (GND 2) ────[ Anti-pad ]──────────●────────── (GND Plane)
         │                                    │
Layer 6  ●═════════ (Internal Trace)
```

- **換層伴隨地過孔約束**：
  - 高速差分信號（PCIe, USB3, SerDes）每處換層過孔兩側，**必須配置至少 1~2 顆接地伴隨過孔 (Stitching Via)**。
  - 伴隨過孔與信號過孔中心間距 $\le 25\,\text{mil}$，確保高頻回流電流無縫切換參考地平面。
- **過孔殘樁消除 (Backdrilling / Stub Removal)**：
  - 當信號速率 $\ge 5\text{ Gbps}$ 時，過孔殘樁長度 ($Stub$) 必須 $\le 10\,\text{mil}$，必要時執行背鑽工藝。

### 3.2 高速走線拓撲與等長約束 (Length Matching & Skew Budget)
| 介面類型 | 走線最大長度 | 差分對內等長 (Intra-pair Skew) | 差分對間等長 (Inter-pair) | 隔離間距 (Crosstalk Spacing) |
| :--- | :---: | :---: | :---: | :---: |
| **PCIe Gen3 (8 GT/s)** | $\le 8.0\text{ inch}$ | $\le 5.0\text{ mil}$ ($< 0.8\text{ ps}$) | 不作嚴格約束 | $\ge 4W$ (或 $30\text{ mil}$) |
| **USB 3.0 (5 Gbps)** | $\le 5.0\text{ inch}$ | $\le 5.0\text{ mil}$ | -- | $\ge 4W$ |
| **DDR4 (2400 MT/s)** | $\le 3.0\text{ inch}$ | DQ-DQS $\le 10.0\text{ mil}$ | Address/Cmd $\le 50.0\text{ mil}$ | $\ge 3W$ |
| **RGMII GbE** | $\le 6.0\text{ inch}$ | TX/RX Clk vs Data $\le 50.0\text{ mil}$| -- | $\ge 3W$ |

---

## 4. ⚡ 電源完整性 (PDN) 鋪銅與去耦電容佈局 (PDN & Decoupling Topology)

### 4.1 電源平面阻抗與高頻去耦原則
- **高 $di/dt$ 迴路最小化**：
  - DC-DC 輸入去耦電容 ($0.1\,\mu\text{F} + 10\,\mu\text{F}$) 必須緊貼晶片 $V_{IN}$ 與 PGND 引腳，走線無過孔直連焊盤。
- **電源層與地層緊密耦合 (Power-Ground Inter-plane Capacitance)**：
  - L4 (PWR) 與 L5 (GND) 介質厚度控制在 $8.0\text{ mil}$ 內，提供天然的高頻平面分佈電容，降低高頻 PDN 阻抗。
- **去耦電容打孔配置 (Via Placement)**：
  - 嚴禁引線過長（Stub），採用雙過孔並聯（Side-by-side Vias）或焊盤內打孔（Via-in-Pad），降低寄生電感 $< 0.5\,\text{nH}$。

---

## 5. 📋 原理圖與 Layout Freeze 核心防呆檢核表 (Design Review Gate Checklist)

### 5.1 原理圖凍結檢核表 (Schematic Freeze Checklist)
- [ ] **元件降額審查**：所有電容耐壓 $\ge 1.33\times$ 工作電壓；電阻/MOSFET 功耗 $\le 60\%$ AMR。
- [ ] **特殊引腳配置**：未使用的晶片引腳依手冊接地、上拉或懸空；Bootloader/ strapping 引腳電平確認無誤。
- [ ] **去耦電容配置**：每個 IC 電源引腳均配置 $0.1\,\mu\text{F}$ 陶瓷去耦電容。
- [ ] **測試點預留 (DFT)**：關鍵電源軌、JTAG、SWD、UART Debug 均配置標準測試點 (Test Point)。

### 5.2 Layout 凍結檢核表 (Layout Freeze Checklist)
- [ ] **高頻回流檢驗**：所有差分線與時鐘線沿途參考平面完整，100% 無跨分割。
- [ ] **接地過孔陣列**：晶片底部 Thermal Pad 下方打滿散熱過孔陣列（孔徑 0.3mm，間距 1.0mm）。
- [ ] **差分對等長補償**：蛇形繞線在失配源頭處就近補償，單次補償高度 $\le 3\times$ 走線寬度。
- [ ] **DFM 裝配裕度**：元件與板邊距離 $\ge 0.5\text{mm}$；MARK 點對角放置；BGA 區域無露銅錫珠隱患。

---

## 6. 📚 關聯專案、Gerber 歸檔與文獻 (Related Specs & References)

- **所屬研發專案 (Project)**：
  - `[[10_Projects/2026-新一代邊緣計算主板研發專案]]`
- **硬體架構與電源規格 (Architecture)**：
  - `[[30_Resources/02_Permanent/Hardware/Architecture/邊緣計算主板系統架構與電源樹規劃]]`
- **晶片選型卡 (Components)**：
  - `[[30_Resources/02_Permanent/Hardware/Components/TI_TPS548D22_Buck]]`
- **板廠 Gerber 與生產工單 (CAM / Fabrication Output)**：
  - `[[90_System/Attachments/PCB_Gerber_EVT_RevA.zip]]`
