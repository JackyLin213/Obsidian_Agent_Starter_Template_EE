---
title: "<% tp.file.title %>"
type: permanent
status: active
tags:
  - Hardware/Component
  - Hardware/Component/Power # 請依類別替換: Power | Interface | Processor | Discrete | Passive | Sensor | Connector
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
part_number: "<% tp.file.title %>"
manufacturer: "TI" # TI | ADI | MPS | Infineon | NXP | ST | Renesas | Microchip | Murata | Vishay
category: "Power/DC-DC" # Power/DC-DC | Power/LDO | Interface/PHY | Processor/MCU | Discrete/MOSFET | Passive/Capacitor | Passive/Inductor | Sensor | Connector
package: "QFN-32 (5x5mm, 0.5mm pitch)"
pin_count: "32"
temp_grade: "Industrial (-40°C ~ +125°C)" # Commercial (0~70°C) | Industrial (-40~85°C/125°C) | Automotive (AEC-Q100)
lifecycle_status: "Active" # Active | Preview | NRND (Not Recommended) | EOL (End of Life)
second_source_status: "Available (Drop-in)" # Available (Drop-in) | Functional Equivalent | Single Source (High Risk)
lead_time_weeks: "12"
unit_price_usd: "$1.25 (1k qty)"
datasheet_url: ""
aliases: []
sources: []
up: "[[30_Resources/03_MOCs/MOC - 元件庫與晶片選型 (Components)]]"
---

# ⚡ <% tp.file.title %> 元件規格與設計指南

> [!ABSTRACT] ⚡ 30 秒選型評估速讀 (Selection Verdict / TL;DR)
> - 🌟 **核心選型優勢 (Pros)**：
> - ⚠️ **主要限制與設計坑點 (Cons & Traps)**：
> - 🔄 **替代料供應鏈現況 (Second Sourcing)**：`second_source_status` (交期：`lead_time_weeks` 週)
> - 🏷️ **推薦應用場景 (Recommended Use Cases)**：
> - 📋 **基本概覽**：`part_number` | **原廠**：`manufacturer` | **封裝**：`package` (`pin_count` Pin, `temp_grade`) | **單價**：`unit_price_usd` | [原廠手冊連結](datasheet_url)

---

## 1. 📋 核心電氣參數與工程降額評估 (Key Electrical Specs & Derating Analysis)

> [!TIP] 🔬 首席架構師降額審查準則 (Derating Baseline)
> - **耐壓降額 (Voltage Derating)**：$\le 75\%$ AMR 極限
> - **功率與電流熱降額 (Power/Current Derating)**：$\le 60\%$ AMR 極限
> - **工作結溫上限 (Max Junction Temp)**：$T_J \le 105^\circ\text{C}$（嚴格保護以確保 MTBF 壽命）

### 電氣參數與安全操作區 (SOA) 檢核表
| 參數名稱 (Parameter) | 符號 | 絕對最大額定 (AMR) | 推薦工作條件 (Rec. Op) | 降額安全上限 (Derated Limit) | 本設計應用值 (Applied) | 設計裕度 (Margin) | 備註與測試條件 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **輸入電壓 (Input Voltage)** | $V_{IN}$ | $20.0\text{ V}$ | $4.5 \sim 18.0\text{ V}$ | $\le 15.0\text{ V}$ ($75\%$ AMR) | $12.0\text{ V}$ | $+20.0\%$ | 滿足 75% 耐壓降額 |
| **輸出電壓範圍** | $V_{OUT}$ | $-0.3 \sim 6.0\text{ V}$ | $0.6 \sim 5.5\text{ V}$ | $\le 4.5\text{ V}$ | $3.3\text{ V}$ | $+26.7\%$ | 支援外部電阻分壓 |
| **最大連續輸出電流** | $I_{OUT}$ | $14.0\text{ A}$ | $12.0\text{ A}$ | $\le 8.4\text{ A}$ ($60\%$ AMR) | $6.0\text{ A}$ | $+28.6\%$ | 滿足 60% 功率降額 |
| **工作結溫 (Junction Temp)** | $T_J$ | $+150^\circ\text{C}$ | $-40 \sim +125^\circ\text{C}$ | $\le 105^\circ\text{C}$ | $82^\circ\text{C}$ (估算) | $+21.9\%$ | $\theta_{JA} = 32^\circ\text{C/W}$ |
| **開關頻率 (Switching Freq)** | $f_{SW}$ | $2.2\text{ MHz}$ | $500\text{k} \sim 1.5\text{ MHz}$ | $1.2\text{ MHz}$ | $800\text{ kHz}$ | 最佳效率點 | 外部電阻設定 |
| **靜態工作電流 (Quiescent)** | $I_Q$ | $300\,\mu\text{A}$ | $150\,\mu\text{A}$ | -- | $135\,\mu\text{A}$ | -- | 低功耗待機評估 |

---

## 2. 💡 典型應用電路與外圍模組計算 (Typical Circuit & Sizing)

### 2.1 典型功能電路架構 (Functional Circuit Diagram)
```
         VIN ────┬──────[ VIN ]──────────┐
                [C_IN]                   │
                 │                   [ SW ] ───[ L_OUT ]───┬──── VOUT
                GND                      │                 │
                                     [ D / FET ]         [C_OUT]
                                         │                 │
                                        GND               GND
```

---

### 2.2 模組化外圍選型計算 (依元件類別選用或自訂)

#### ⚡ 模組 A：電源轉換類 (DC-DC Buck / Boost / LDO)
- **電感值計算 ($L_{OUT}$)**：
  $$L = \frac{V_{OUT} \times (V_{IN} - V_{OUT})}{V_{IN} \times f_{SW} \times \Delta I_L}$$
  *其中電感紋波電流比 $\Delta I_L$ 通常設定為 $I_{OUT}$ 的 $20\% \sim 40\%$。*
- **輸出電容與 ESR 零點頻率 ($C_{OUT}$)**：
  $$f_{z\_esr} = \frac{1}{2\pi \cdot R_{ESR} \cdot C_{OUT}}$$
- **反饋分壓電阻 ($R_{top}, R_{bot}$)**：
  $$V_{OUT} = V_{REF} \times \left(1 + \frac{R_{top}}{R_{bot}}\right)$$

#### 🌊 模組 B：高速介面與 PHY 類 (PCIe / Ethernet / USB / SerDes)
- **差分阻抗控制**：$Z_{diff} = 100\,\Omega \pm 10\%$（單端 $50\,\Omega$）
- **AC 耦合電容 (AC-Coupling Cap)**：$0.1\,\mu\text{F}$ 0402 X7R 規格，對稱放置於發送端 (TX) 或接收端 (RX)
- **ESD 防護器件寄生電容約束**：$C_{diode} \le 0.3\,\text{pF}$（防止信號上升沿退化與眼圖閉合）

#### 🔌 模組 C：功率開關類 (MOSFET / Load Switch)
- **導通損耗 (Conduction Loss)**：$P_{cond} = I_{rms}^2 \times R_{DS(on)}$
- **開關損耗 (Switching Loss)**：$P_{sw} = \frac{1}{2} V_{IN} \cdot I_{OUT} \cdot (t_r + t_f) \cdot f_{sw}$
- **閘極驅動電阻選型 ($R_G$)**：平衡 EMI 噪訊與開關速度

#### 📦 模組 D：被動元件特性與偏壓衰減 (Passives & MLCC DC Bias)
- **MLCC 直流偏壓容量衰減 (DC Bias Derating)**：
  ⚠️ *注意：高介電常數陶瓷電容 (如 0603/0805 X5R/X7R) 在施加額定直流偏壓時，實際有效容值可能劇降 $50\% \sim 70\%$，需預留足夠裕量！*
- **電感飽和電流餘量**：$I_{sat} \ge 1.3 \times I_{peak}$

---

## 3. ⚠️ 關鍵引腳配置與硬體避坑防呆 (Critical Pin Traps & Pinout Defenses)

### 3.1 封裝引腳空間分佈圖 (Package Pinout Map)
```text
                  +-------------+
        BOOT  [1] |             | [8]  SW
         VIN  [2] |  TOP VIEW   | [7]  GND
          EN  [3] | (SOIC / QFN | [6]  COMP
        VCC5  [4] |  Pin Map)   | [5]  FB
                  +-------------+
```

### 3.2 特殊引腳致命錯誤防呆表 (Deadly Pin Traps)
> [!CAUTION] 🚨 特殊引腳致命錯誤防呆表 (Deadly Pin Traps)

| Pin 名稱 | Pin 類型 | 推薦標準連接方式 | ❌ 常見致命硬體陷阱 (Deadly Trap) | 檢查狀態 |
| :--- | :---: | :--- | :--- | :---: |
| **EP / Thermal Pad** | Power GND | 裸露焊盤打滿地過孔直通主 GND 平面 | ❌ 誤接為懸空或接至 Signal GND，導致 IC 散熱不良迅速過熱保護 | [ ] |
| **BOOT / BST** | High-Side Drive | 串接 $0.1\,\mu\text{F}$ 陶瓷電容 + $2.2\,\Omega$ 電阻至 SW | ❌ 串聯電阻過大或電容耐壓不足，導致高側 MOSFET 無法完全導通 | [ ] |
| **FB / SENSE** | Analog Input | 緊貼 IC 引腳，分壓電阻就近擺放，走內層地屏蔽 | ❌ 走線直接穿越 SW Node 高 $dv/dt$ 噪訊區，導致輸出電壓大幅跳動 | [ ] |
| **EN / UVLO** | Logic Input | 外部電阻分壓設定精確欠壓鎖定閾值 | ❌ 直接浮空 (Floating) 導致啟動狀態未定義或隨空間噪訊誤觸發 | [ ] |
| **MODE / SYNC** | Configuration | 依所需工作模式 (FPWM/DCM) 接至 VCC 或 GND | ❌ 阻抗過高或懸空導致輕載工作模式在 PFM 與 PWM 間異常切換 | [ ] |
| **NC (No Connect)** | Internal Pin | 依原廠手冊要求嚴格保持懸空 (Floating) | ❌ 誤將內部測試引腳接地造成晶片短路或內部邏輯死鎖 | [ ] |

---

## 4. ⚠️ 關鍵 PCB Layout 與 SI/PI/Thermal 佈線指南 (Critical Layout Rules)

> [!WARNING] 原廠 Layout 核心避坑重點
> 1. **高頻開關迴路 (High-di/dt Loop 最小化)**：$V_{IN}$ 去耦電容至 GND 迴路必須緊貼晶片引腳，迴路面積 $< 15\,\text{mm}^2$。
> 2. **SW Node (高 dv/dt 節點控制)**：鋪銅面積應在載流足夠前提下盡量縮小，避免對相鄰敏感信號（FB, COMP, 晶振）產生容性耦合串擾。
> 3. **反饋引腳走線 (Feedback Shielding)**：遠離電感與開關節點，走在內層並由完整地平面包覆屏蔽。
> 4. **散熱過孔陣列 (Thermal Vias Array)**：底層 Thermal Pad 下方打至少 $9 \sim 16$ 顆接地過孔（孔徑 0.3mm，孔距 1.0mm），直通主地平面。

---

## 5. 🔄 第二料源與替代料供應鏈評估 (Second Source & Supply Chain Risk)

### 5.1 替代料型號與相容度分析表
| 替代型號 (MPN) | 原廠 (Vendor) | Pin-to-Pin 相容性 | 參數差異與改版風險評估 | 供應鏈交期 / 單價 | 驗證狀態 |
| :--- | :--- | :---: | :--- | :---: | :---: |
| **MPxxxx** | MPS | 🟢 是 (Drop-in) | 封裝與引腳完全一致，需確認環路補償參數穩定度 | 8 週 / $1.10 | [ ] 待驗證 |
| **LTCxxxx** | ADI | 🔴 否 (需改 Layout) | 噪訊更低但引腳定義不同，需重新 Layout 評估 | 16 週 / $2.40 | [ ] 備案 |

### 5.2 供應鏈風險與量產可行性
- **生命週期預警**：`lifecycle_status`（若為 NRND / EOL 需在 3 個月內啟動替代方案）
- **採購交期 (Lead Time)**：`lead_time_weeks` 週 | **最小訂購量 (MOQ)**：$\quad$ pcs
- **車規 / 工規等級認證**：`temp_grade`

---

## 6. 📚 關聯應用手冊 (App Notes)、實務專案與除錯記錄

- **原廠 Application Notes**：
  - `[[@TI_2023_AN-2162_BuckConverterLayoutGuide]]`
- **使用此晶片的專案 (Projects)**：
  - `[[10_Projects/2026-新一代邊緣計算主板研發專案]]`
- **相關除錯記錄 (Debug Notes)**：
  - `[[Debug - 12V轉1V0電源紋波過大問題排查]]`
- **沉澱衍生原子卡片 (Permanent Notes)**：
  - `[[30_Resources/02_Permanent/Hardware/Power/降壓轉換器閉迴路補償設計]]`
