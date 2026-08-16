---
title: "Validation - <% tp.file.title.replace('Validation - ', '') %>"
type: permanent
status: draft # draft | in_progress | completed | conditional_pass | failed
tags:
  - Hardware/Validation
  - Hardware/Test # Hardware/Test | Hardware/Bringup | Hardware/DVT
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
project: "[[10_Projects/專案名稱]]"
board_rev: "DVT" # EVT | DVT | PVT | Pilot Run
board_sn: "DUT-01 ~ DUT-05"
test_stage: "DVT" # Bring-up | EVT | DVT | PVT
test_engineer: "[[人物]]"
overall_verdict: "Pass" # Pass | Fail | Conditional Pass
total_tests: 24
passed_tests: 24
failed_tests: 0
aliases: []
sources: []
up: "[[30_Resources/03_MOCs/MOC - 測試驗收與 EMC 合規認證 (Validation & Compliance)]]"
---

# 🧪 Validation - <% tp.file.title.replace('Validation - ', '') %>

> [!ABSTRACT] ⚡ 30 秒驗收測試結論速讀 (Validation Verdict / TL;DR)
> - 🎯 **測試階段與目標**：`project` (`board_rev`) | **測試階段**：`test_stage`
> - 🏁 **總體驗收結論 (Overall Verdict)**：**`overall_verdict`** (通過率：`passed_tests` / `total_tests`, 異常：`failed_tests`)
> - ⚡ **核心指標摘要**：全電源軌紋波 $\le 25\text{mV}$、高速差分眼圖裕度 $\ge 35\%$、最高結溫 $T_J = 84.2^\circ\text{C} \le 105^\circ\text{C}$
> - 👤 **主測工程師**：`test_engineer` | **報告狀態**：`status`

---

## 1. 📋 測試範圍與待測物 (DUT) 環境配置 (Test Setup & Environment)

### 1.1 待測單板 (DUT) 與韌體版本清單
| 待測板序號 (DUT SN) | 硬體版本 (HW Rev) | 燒錄韌體版本 (FW Ver) | 測試載具 / 夾具 (Fixture) | 備註說明 |
| :--- | :---: | :---: | :--- | :--- |
| **DUT-01** | `board_rev` | `v1.0.0-rc2` | 標準評估底板 (Carrier Board) | 主要電氣性能與信號品質測試 |
| **DUT-02** | `board_rev` | `v1.0.0-rc2` | 高低溫環境箱治具 | 環境可靠度與溫度溫升測試 |
| **DUT-03** | `board_rev` | `v1.0.0-rc2` | 自動化老化治具 (Burn-in) | 72 小時連續滿載壓力測試 |

### 1.2 測試儀器與量測保真度檢核表 (Equipment Setup)
| 儀器名稱 | 廠牌與型號 | 頻寬 / 精度規格 | 校準狀態 | 量測手法 / 探棒防呆確認 |
| :--- | :--- | :---: | :---: | :--- |
| **高頻示波器** | Keysight Infiniium MXR | 4 GHz, 16 GSa/s | 🟢 Valid | 採用接地彈簧 (Ground Spring) 與同軸直連 |
| **主動差分探棒** | Keysight N2751A | 3.5 GHz 差分探頭 | 🟢 Valid | 焊接探頭直連高速差分測試點 |
| **可程式直流負載**| Chroma 63102A | 0~30A, 100A/$\mu$s | 🟢 Valid | 短粗絞線連接，消除引線寄生電感 |
| **紅外熱像儀** | FLIR T540 | 精度 $\pm 1.0^\circ\text{C}$ | 🟢 Valid | 預熱 30 分鐘，發射率設置 0.95 |

---

## 2. 📊 核心電氣性能與信號品質驗證矩陣 (Electrical & Signal Quality Matrix)

### 2.1 電源軌靜態紋波與動態跳載響應 (Power Rails & Transient Response)
| 電源軌名稱 | 標稱電壓 | 靜態紋波實測 ($V_{pk-pk}$) | 規範上限 | 動態跳載條件 ($\Delta I_{step}$) | 動態過沖/下衝 ($\Delta V_{trans}$) | 裕度 (Margin) | 判定 |
| :--- | :---: | :---: | :---: | :--- | :---: | :---: | :---: |
| **5V0_SYS** | $5.00\text{ V}$ | $18.5\text{ mV}$ | $< 30\text{ mV}$ | $1.0\text{A} \leftrightarrow 4.0\text{A}\ (1\text{A}/\mu\text{s})$ | $+120\text{ mV} / -145\text{ mV}$ | $+38.3\%$ | 🟢 Pass |
| **3V3_SYS** | $3.30\text{ V}$ | $14.2\text{ mV}$ | $< 25\text{ mV}$ | $0.5\text{A} \leftrightarrow 3.0\text{A}\ (1\text{A}/\mu\text{s})$ | $+85\text{ mV} / -92\text{ mV}$ | $+43.2\%$ | 🟢 Pass |
| **1V8_SYS** | $1.80\text{ V}$ | $11.0\text{ mV}$ | $< 20\text{ mV}$ | $0.2\text{A} \leftrightarrow 1.5\text{A}\ (1\text{A}/\mu\text{s})$ | $+45\text{ mV} / -50\text{ mV}$ | $+45.0\%$ | 🟢 Pass |
| **0V85_CORE**| $0.85\text{ V}$ | $8.6\text{ mV}$ | $< 15\text{ mV}$ | $2.0\text{A} \leftrightarrow 8.0\text{A}\ (5\text{A}/\mu\text{s})$ | $+28\text{ mV} / -32\text{ mV}$ | $+42.6\%$ | 🟢 Pass |

### 2.2 高速差分信號眼圖與抖動測試 (High-Speed Eye Diagram & Jitter)

> [!NOTE] 👁️ 高速差分眼圖量測波形
> ![[90_System/Attachments/PCIe_Gen3_Eye_Diagram_Pass.png]]
> *波形描述：PCIe Gen3 (8 GT/s) 在滿載連續運行時之接收端眼圖，眼高 168mV，眼寬 0.65 UI，完全避開 Template Mask。*

| 高速信號介面 | 測試速率 | 實測眼高 (Eye Height) | 規範要求 (Spec) | 實測抖動 ($T_j\ @\text{BER }10^{-12}$) | 規範抖動上限 | 判定 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **PCIe Gen3 TX**| 8.0 GT/s | $168\text{ mV}$ | $> 120\text{ mV}$ | $28.5\text{ ps}$ | $< 45\text{ ps}$ | 🟢 Pass |
| **USB 3.0 TX** | 5.0 Gbps | $245\text{ mV}$ | $> 180\text{ mV}$ | $42.0\text{ ps}$ | $< 60\text{ ps}$ | 🟢 Pass |
| **GbE MDI TX** | 1000BASE-T| 符合 IEEE 802.3ab 模板 | Mask Margin $> 25\%$ | -- | -- | 🟢 Pass |

---

## 3. 🌡️ 環境可靠度與溫度溫升測試 (Environmental & Thermal Stress Test)

### 3.1 關鍵晶片表面溫度與工作結溫計算表 (Thermal Dissipation & $T_J$)
> [!TIP] 🔬 工作結溫計算公式：$T_J = T_C + P_{loss} \times \theta_{JC} \le 105^\circ\text{C}$

| 元件位號 (RefDes) | 晶片型號 / 功能 | 表面溫度 ($T_C\ @ 25^\circ\text{C}$) | 極限環境表面溫 ($T_C\ @ 55^\circ\text{C}$) | 熱阻 ($\theta_{JC}$) | 計算結溫 ($T_J\ @ 55^\circ\text{C}$) | 降額安全門檻 | 判定 |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **U1** | 主控 SoC | $52.4^\circ\text{C}$ | $78.6^\circ\text{C}$ | $3.5^\circ\text{C/W}$ | **$88.4^\circ\text{C}$** | $\le 105^\circ\text{C}$ | 🟢 Pass |
| **U12** | 12V轉5V 主 Buck | $48.2^\circ\text{C}$ | $74.5^\circ\text{C}$ | $4.2^\circ\text{C/W}$ | **$82.1^\circ\text{C}$** | $\le 105^\circ\text{C}$ | 🟢 Pass |
| **U15** | Core PMIC 多相電源 | $55.1^\circ\text{C}$ | $81.2^\circ\text{C}$ | $2.8^\circ\text{C/W}$ | **$87.0^\circ\text{C}$** | $\le 105^\circ\text{C}$ | 🟢 Pass |

### 3.2 極限環境與長時間老化測試 (Environmental Trials)
- [x] **低溫冷開機 (Cold Boot @ $-40^\circ\text{C}$)**：連續開關機 50 次，100% 正常進入系統，時鐘晶振起振正常。
- [x] **高溫滿載老化 (Burn-in @ $+70^\circ\text{C}$, 72 hrs)**：無當機、無重啟、系統無 Memory Leak 或封包錯誤。
- [x] **熱插拔衝擊 (Hot-Plug ESD & Inrush)**：USB/Type-C 連續熱插拔 100 次，未觸發過流保護鎖死。

---

## 4. 🤖 自動化測試腳本與數據日誌 (Automated Test Execution & Logs)

### 4.1 Python / SCPI 自動化測試腳本 (Automation Script)
```python
# ==============================================================================
# Hardware DVT Validation Suite: Power Ripple & Voltage Sweep
# ==============================================================================
import pyvisa
import time

def run_dvt_power_sweep():
    rm = pyvisa.ResourceManager()
    scope = rm.open_resource("TCPIP0::192.168.1.100::inst0::INSTR")
    eload = rm.open_resource("TCPIP0::192.168.1.101::inst0::INSTR")
    
    print("[INFO] Starting DVT automated power sweep on VDD_CORE...")
    for current in [1.0, 3.0, 6.0, 8.0]:
        eload.write(f"CURR:STAT:L1 {current}")
        time.sleep(1.0)
        v_rip = float(scope.query(":MEASure:VRMS? CHAN1"))
        print(f"  Load: {current}A | Measured RMS Ripple: {v_rip*1000:.2f} mV")
        assert v_rip < 0.015, f"FAIL: Ripple exceeded 15mV limit at {current}A"
    print("[SUCCESS] All power rails passed DVT automated test suite.")

if __name__ == "__main__":
    run_dvt_power_sweep()
```

---

## 5. 🚨 測試異常 (Anomalies) 與 Issue 追蹤 (Issue Tracking)

| 異常編號 | 發現測項 | 異常現象簡述 | 嚴重度 | 關聯除錯記錄 (Debug Note) | 處置狀態 |
| :---: | :--- | :--- | :---: | :--- | :---: |
| **ISS-01** | 動態負載跳階 | 12V 轉 1V0 輕載切換時開關節點有震鈴 | Major | `[[Debug - 12V轉1V0電源紋波過大問題排查]]` | 🟢 已導入 Snubber 解決 |

---

## 6. 🏁 階段門放行簽核與驗收結論 (Stage-Gate Sign-off)

> [!IMPORTANT] 🏁 DVT 階段門簽核評定
> - **評審結論**：🟢 **通過 (Passed - Ready for PVT / Pilot Run)**
> - **放行依據**：全板 24 項硬體電氣與可靠度指標全部達標，降額評估符合 $T_J \le 105^\circ\text{C}$ 與 $60\%$ 負載規範。
> - **簽核人員**：硬體負責人 `test_engineer`、系統架構師、專案經理 (PM)。

---

## 7. 📚 關聯專案與設計文件 (Related Links)

- **所屬研發專案 (Project)**：
  - `[[10_Projects/2026-新一代邊緣計算主板研發專案]]`
- **硬體架構與規格 (Architecture)**：
  - `[[30_Resources/02_Permanent/Hardware/Architecture/邊緣計算主板系統架構與電源樹規劃]]`
- **PCB 疊構與走線 (PCB Stackup)**：
  - `[[30_Resources/02_Permanent/Hardware/PCB/8層高速運算主板疊構與阻抗規格]]`
