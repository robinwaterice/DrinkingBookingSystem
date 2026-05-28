# 🧋 辦公室午後救星 - 當日飲料訂購系統

[![Vite](https://img.shields.io/badge/Vite-6.x-646CFF.svg?logo=vite)](https://vite.dev/)
[![React](https://img.shields.io/badge/React-18.x-61DAFB.svg?logo=react)](https://react.dev/)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-v4-06B6D4.svg?logo=tailwindcss)](https://tailwindcss.com/)
[![Database](https://img.shields.io/badge/Database-Google%20Sheets-34A853.svg?logo=googlesheets)](https://www.google.com/sheets/about/)

一個精美、流暢且高質感的「辦公室當日飲料訂購系統」。專為解決辦公室集體點單痛點而設計，具備即時統計分析與自動化雲端同步功能。前端採用 React 搭配 Tailwind CSS 構建，後端使用 Google Apps Script (GAS) 串接 Google 試算表，無需複雜伺服器即可隨插即用！

---

## ✨ 核心特色

* 🍵 **精美推薦菜單牆**：即時分類篩選與品項詳細介紹，支援一鍵點擊快速將飲品帶入表單。
* ✏️ **客製化點單系統**：支援訂購人姓名記憶、杯數調整、多種配料加點（珍珠、椰果、仙草凍、贅澤布丁），以及經典的糖度與冰量選擇。
* 📈 **即時點單統計看板**：
  * 即時計算今日累計杯數、消費總額與訂購人數。
  * 熱門飲品 Top 3 自動排行。
  * 糖度、冰量偏好比例的動態進度條分析。
* ☁️ **雲端試算表後端**：點單自動同步寫入 Google 試算表。支援直接在網頁名冊上「編輯」或「刪除」今日點單，雙向即時對齊。
* 💾 **離線與防呆降級機制**：在網路異常或後端響應慢時，自動啟用離線備份菜單與本地 mock 機制，保證點單操作不卡頓。

---

## 🛠️ 本地運行與開發

**系統需求**：安裝 [Node.js](https://nodejs.org/) 環境。

### 1. 安裝套件
在專案根目錄執行以下指令安裝開發依賴：
```bash
npm install
```

### 2. 本地啟動開發伺服器
```bash
npm run dev
```
啟動後在瀏覽器開啟 `http://localhost:3000` 即可檢視並使用訂購系統。

### 3. 生產環境建置
```bash
npm run build
```

---

## ☁️ 後端 Google 試算表部署說明

本系統後端使用 **Google Apps Script (GAS)** 將 Google 試算表發佈為 API 提供給前端呼叫。如果您想部署自己專屬的試算表後端，請參考以下步驟：

1. **建立試算表**：在您的雲端硬碟建立一個新的 Google 試算表。
2. **新增工作表**：
   * 建立一個工作表命名為 `Menu`（包含欄位：`name`, `price`, `category`, `description`）作為菜單設定。
   * 建立另一個工作表命名為 `Orders`（包含欄位：`orderId`, `timestamp`, `name`, `drink`, `sugar`, `ice`, `quantity`, `totalPrice`）用於記錄訂單。
3. **編寫 Script**：
   * 在試算表中點擊「擴充功能」 > 「Apps Script」。
   * 寫入對應的 `doGet` 與 `doPost` 方法處理 JSON 資料讀寫，並發佈為「Web 應用程式」（權限設為「任何人」）。
4. **串接前端**：
   * 將發佈產生的 Web 應用程式網址，複製並替換 `index.html` 第 87 行中的 `API_URL` 變數：
     ```javascript
     const API_URL = "https://script.google.com/macros/s/您的部署ID/exec";
     ```

---

## 📄 專案授權

本專案採用開源授權，歡迎自由修改並部署為您辦公室的午後救星！
