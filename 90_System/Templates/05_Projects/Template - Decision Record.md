---
title: "ADR - <% tp.file.title.replace('ADR - ', '') %>"
type: permanent
status: evergreen
tags:
  - Decision/ADR
  - Hardware/Architecture/<% tp.file.title.replace('ADR - ', '') %>
created: "<% tp.file.creation_date('YYYY-MM-DD HH:mm:ss') %>"
updated: "<% tp.file.last_modified_date('YYYY-MM-DD HH:mm:ss') %>"
decision_status: "Accepted" # Proposed | Accepted | Rejected | Superseded | Deprecated
decision_date: "<% tp.date.now('YYYY-MM-DD') %>"
decision_makers:
  - "[[人物名稱]]"
review_date: "<% tp.date.now('YYYY-MM-DD', 'P6M') %>"
project: "[[10_Projects/專案名稱]]"
category: "Power Topology" # Power Topology | PHY / SerDes Selection | PCB Stacking | Thermal Architecture | Protection
impact_level: "High" # High (BOM/Architecture) | Medium (Layout/Component) | Low (BOM Alt)
superseded_by: ""
aliases:
  - "<% tp.file.title.replace('ADR - ', '') %> 決策記錄"
sources: []
up: "[[30_Resources/03_MOCs/MOC - 架構與決策]]"
---

# ⚖️ ADR - <% tp.file.title.replace('ADR - ', '') %>

> [!NOTE] 📋 決策核心看板 (Decision Executive Summary)
> - **決策狀態**：`decision_status` ｜ **決策日期**：`decision_date` ｜ **覆盤日期**：`review_date`
> - **架構分類**：`category` ｜ **影響層級**：`impact_level` ｜ **關聯專案**：`project`
> - **決策者**：`decision_makers`
> - **一分鐘核心結論**：簡述最終選定的技術方案及其最關鍵的勝出理由。

---

## 🔍 1. 背景與問題陳述 (Context & Problem Statement)

### 業務與工程痛點
- 描述觸發此技術決策的根本瓶頸（例如：散熱極限、電源紋波過大、PCB 佔板面積受限、晶片缺貨或交期過長）。

### 核心硬體約束條件 (Design Constraints)
1. **電氣性能約束**：輸入電壓範圍 $V_{IN}$、輸出電流負載 $I_{OUT}$、紋波容限 $\Delta V \le 2\%$。
2. **熱與空間約束**：板卡高度限制 $\le 5\text{mm}$、環境溫度 $T_A = 50^\circ\text{C}$ 下結溫 $T_J \le 105^\circ\text{C}$。
3. **成本與供應鏈約束**：單路電源 BOM 預算 $\le \$1.50\text{ USD}$，交期 $\le 16\text{ 週}$，必須具備相容的 Second-Source。

---

## 📊 2. 備選方案評估與權衡矩陣 (Options Evaluation & Trade-offs)

### 2.1 方案效益與複雜度象限圖 (Trade-offs Quadrant Chart)
```mermaid
quadrantChart
    title 方案效益與實施複雜度評估
    x-axis 低複雜度/低成本 --> 高複雜度/高成本
    y-axis 低效益/低效能 --> 高效益/高效能
    quadrant-1 🏆 最佳平衡 (Best Fit)
    quadrant-2 ⚡ 快速方案 (Quick Wins)
    quadrant-3 ❌ 不予考慮 (Drop)
    quadrant-4 ⚠️ 高風險高成本 (High Risk)
    "方案 A (傳統非同步)": [0.2, 0.3]
    "方案 B (同步降壓)": [0.4, 0.85]
    "方案 C (整合模組)": [0.85, 0.9]
```

### 2.2 方案定量對比矩陣 (Comparison Matrix)

| 評估維度 | 方案 A: [方案名稱] | 方案 B: [方案名稱] | 方案 C: [方案名稱] | 判定標準 / 權重 |
| :--- | :--- | :--- | :--- | :---: |
| **拓撲架構** | 傳統非同步降壓 (Buck) | 高頻同步降壓 (Sync Buck) | 整合型電源模組 (Power Module) | 架構成熟度 (20%) |
| **BOM 成本** | 🟢 **$0.65** (低) | 🟡 **$1.10** (中) | 🔴 **$2.80** (高) | 成本預算 (25%) |
| **轉換效率** | 🔴 82% (損耗大) | 🟢 **93%** (優異) | 🟢 **94%** (優異) | 散熱與功耗 (25%) |
| **佔板面積** | 🔴 $150\text{ mm}^2$ (需外接二極體) | 🟢 **$65\text{ mm}^2$** | 🟢 **$40\text{ mm}^2$** (最高整合度) | 空間約束 (15%) |
| **供應鏈風險** | 🟢 現貨充足 / 多廠商 | 🟢 2 家原廠 Pin-to-Pin 相容 | 🔴 單一供應商獨家 (Sole Source) | 供應鏈安全 (15%) |
| **綜合評分** | 68 分 | 🏆 **92 分** | 76 分 | 100% |

---

### 各方案質化細節分析

#### 方案 A：[方案名稱]
- 🟢 **優點 (Pros)**：成本極低，市場流通量大。
- 🔴 **缺點 (Cons)**：非同步續流二極體壓降大，高溫滿載時二極體發熱嚴重，無法滿足 $T_J \le 105^\circ\text{C}$ 降額規範。

#### 方案 B：[方案名稱] (選定方案)
- 🟢 **優點 (Pros)**：內建低 $R_{DS(on)}$ 上下管 MOSFET，效率高，支援 $2.2\text{MHz}$ 開關頻率避開 AM 頻段干擾，具備 Pin-to-Pin 替代晶片。
- 🔴 **缺點 (Cons)**：周邊開關迴路佈局需極度緊湊，防止高 $di/dt$ 振鈴。

#### 方案 C：[方案名稱]
- 🟢 **優點 (Pros)**：電感整合封裝，設計極度簡單，面積最小。
- 🔴 **缺點 (Cons)**：單價超過預算 85%，且無 Second Source，產能斷料風險過高。

---

## 🏆 3. 最終決策結果與技術依據 (Decision & Rationale)

> **決定採納：方案 B（[方案名稱]）**

### 核心定案理由：
1. **熱與效率合規**：滿載效率 $93\%$ 確保在 $50^\circ\text{C}$ 環境下結溫僅 $82^\circ\text{C}$，完全滿足降額標準。
2. **空間與成本平衡**：$65\text{ mm}^2$ 佔板面積符合機構限制，且 BOM 成本 $\$1.10$ 低於預算上限。
3. **供應鏈韌性**：TI 與 MPS 具備 Pin-to-Pin 相容料號，具備雙來源保障。

---

## ⚠️ 4. 預期後果、風險與緩解對策 (Consequences & Mitigations)

| 預期影響 / 風險點 | 衝擊等級 | 預防與緩解對策 (Mitigation Plan) | 責任人 |
| :--- | :---: | :--- | :---: |
| 高頻開關 $di/dt$ 產生 EMI 輻射噪訊 | 中 (Medium) | 輸入電容緊貼 VIN/GND 引腳；預留 SW 節點 RC Snubber 焊盤 | 👤 EE |
| SW 節點震盪影響周邊敏感走線 | 低 (Low) | Layout 限制 SW 銅皮面積最小化，且底層配置完整 GND 屏蔽 | 👤 Layout |

---

## 🧪 5. 工程驗證與驗收標準 (V&V Criteria)

為驗證此架構決策之正確性，將於 EVT 階段執行以下驗收實驗：
- [ ] 📈 **效率與溫升曲線**：於溫度箱內量測 $25^\circ\text{C}$ 與 $50^\circ\text{C}$ 條件下 $0.1\text{A} \sim 3\text{A}$ 效率曲線。
- [ ] 🔬 **SW 節點電壓應力**：示波器滿載抓取 SW 振鈴峰值，確認 $V_{peak} \le 0.85 \times V_{DS\_max}$。
- [ ] 🛡️ **BOM 雙料驗證**：在 EVT2 批次上線 SMT 驗證 Second-Source 晶片之動態響應。

---

## 🔄 6. 下游設計變更與 ECO 連動 (Implementation & ECO)

- **原理圖變更**：更新 Page 04 電源架構，替換為方案 B 符號與周邊補償電路。
- **PCB 佈線約束**：加入 High di/dt Loop 規則群組，設定輸入電容至 IC 走線距離 $\le 1.0\text{mm}$。
- **韌體/控制**：無軟體相依性（純硬體自動調節）。

---

## 🔁 7. 週期性覆盤記錄 (Post-Decision Review)
> 預計於 `review_date` 進行覆盤：
- **實際運作評估**：
- **是否需要重構或被新 ADR 取代**：
