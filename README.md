# 匯率換算器 Currency Converter

一個即時匯率換算的網頁應用，串接 ExchangeRate API 取得每日更新的匯率，支援多國幣別互相換算。

🔗 **線上 Demo**：https://jojo920912-maker.github.io/currency-converter/

## 功能特色

- 💱 **即時匯率換算**：串接 ExchangeRate API，取得最新匯率資料
- 🌍 **多幣別支援**：支援世界各國貨幣互相換算
- 🕐 **每日更新**：顯示匯率最後更新時間
- 📱 **響應式設計（RWD）**：支援桌機、平板、手機各種螢幕尺寸

## 使用技術

- **Vue 3**（Composition API）
- **Vite**
- **Axios** — 串接外部 API
- **ExchangeRate API** — 即時匯率資料來源

## 本機執行

### 1. 下載專案

```sh
git clone https://github.com/jojo920912-maker/currency-converter.git
cd currency-converter
```

### 2. 安裝套件

```sh
npm install
```

### 3. 設定環境變數

本專案使用 ExchangeRate API，需要自行申請 API Key。

請至 [ExchangeRate-API](https://www.exchangerate-api.com/) 申請免費 API Key，並在專案根目錄建立 `.env` 檔案，填入：