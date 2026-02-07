# 🛡️ MAGI SYSTEM // 曜日天梯榜
### SOLAR CUP LEAGUE RANKING SYSTEM

![Version](https://img.shields.io/badge/MAGI_SYS-VER.20.0-9d5df2?style=for-the-badge)
![Status](https://img.shields.io/badge/STATUS-OPERATIONAL-39ff14?style=for-the-badge)

**MAGI SYSTEM** 是一個極具視覺衝擊力的羽球聯賽天梯排名系統。
靈感源自《新世紀福音戰士》(EVA) 的 MAGI 超級電腦介面，本系統專為「曜日羽球團」設計，將選手數據轉化為駕駛員同步率，提供沉浸式的戰績查詢體驗。

---

## ⚡ 核心機能 (System Capabilities)

### 1. 戰術儀表板 (Tactical Dashboard)
- **EVA 風格 UI**：包含掃描線、霓虹光暈、動態格線背景與戰術字體 (Orbitron)。
- **響應式設計**：完美支援桌機與手機 (Mobile) 介面，手機版自動優化欄位寬度與按鈕排列。

### 2. 駕駛員資料庫 (Pilot Database)
- **即時排名**：依據積分 (Sync Rate) 自動排序。
- **階級過濾**：快速切換 白金 (Platinum) / 黃金 (Gold) / 白銀 (Silver) / 青銅 (Bronze) 級別。
- **智慧檢索**：支援搜尋 **ID 編號**、**姓名** 或 **所屬球團**。

### 3. 詳細分析模式 (Analysis Mode)
- **3D 戰術卡片**：點擊列表可開啟詳細卡片，支援滑鼠懸停的 3D 視差效果。
- **雷達圖分析**：根據積分自動生成 ATK / DEF / SPD / TEC 四維能力雷達圖。
- **自動球團識別**：系統透過雜湊演算法 (Hash-to-Color)，自動為不同球團生成專屬霓虹色，無需手動設定。

### 4. 戰鬥履歷 (Battle Log)
- **歷屆戰績**：卡片內建可捲動的歷史戰績欄位。
- **智能顯示**：自動將選手目前的級別與歷史名次結合顯示 (如：`白金級 冠軍`)。

---

## 📊 資料來源配置 (Data Configuration)

本系統採 **Serverless** 架構，直接讀取 **Google Sheets (試算表)** 發布的 CSV 檔案。

### 1. 試算表結構
請確保您的 Google Sheet 欄位順序如下：

| 欄位 A | 欄位 B | 欄位 C | 欄位 D | 欄位 E | 欄位 F ~ Z... |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ID** | **姓名** | **球團** | **級別** | **積分** | **歷史戰績 (可無限新增)** |
| 4803 | 阿達 | 歡樂 | 白金級 | 400 | 冠軍 |
| 1761 | 湯包 | 歡樂 | 白金級 | 380 | 亞軍 |

> **注意**：
> - **ID**：可以是數字或文字，系統會強制轉為文字處理以避免錯誤。
> - **級別**：需包含「白金」、「黃金」、「白銀」、「青銅」關鍵字以觸發對應邊框顏色。
> - **歷史戰績**：F欄之後的所有欄位都會被讀取為該選手的歷屆戰績 (CUP-01, CUP-02...)。

### 2. 連結設定
在 `index.html` 的 `<script>` 區塊頂端，替換您的 CSV 連結：

```javascript
const CSV_URL = "您的_GOOGLE_SHEET_CSV_發布連結";
