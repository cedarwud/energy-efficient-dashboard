# 能源高效儀表板

一個能源高效的儀表板網頁應用程式，實時可視化來自 USRP B210 和 AWR1642BOOST-ODS 等設備的數據。該儀表板使用互動式的儀錶圖監控功耗、電流、電壓和累積功率。它使用 Next.js 進行服務端渲染，React 用於前端 UI，Socket.IO 用於實時通信，MySQL 用於數據存儲。

## 功能

- **實時數據可視化**：使用儀錶圖實時顯示功耗、電流、電壓和累積功率。
- **互動式儀表板**：提供直觀的界面，具有動畫和響應式設計，適用於各種屏幕尺寸。
- **設備模擬**：可視化設備交互，包括基站和移動汽車，以模擬基於距離的調整。
- **Socket.IO 集成**：實現服務器和客戶端之間的實時通信，進行即時數據更新。
- **MySQL 數據庫連接**：從 MySQL 數據庫中獲取並顯示數據，實現持久化存儲。

## 項目結構

.eslintrc.json
.gitignore
eslint.config.js
next.config.mjs
package.json
server.js
src/
  app/
    api/
      get-distance/
        route.js
    assets/
      css/
        base-station.css
        dashboard.css
      images/
    components/
      base-station.tsx
      dashboard.tsx
    fonts/
    globals.css
    layout.tsx
    page.tsx
tsconfig.json

## 先決條件

- **Node.js**（版本 14 或更高）
- **MySQL** 數據庫
- **npm** 套件管理器

## 安裝

1. **克隆倉庫：**

   ```bash
   git clone https://github.com/cedarwud/energy-efficient-dashboard.git

2. 導航到項目目錄：

cd energy-efficient-dashboard

3. 安裝依賴項：
npm install

配置
數據庫設置
創建 MySQL 數據庫：

創建一個名為 radarDb 的數據庫。
創建一個具有必要結構的表 radartousrp。
更新數據庫憑據：

修改 route.js 中的數據庫連接設置：
const connection = await mysql.createConnection({
  host: "localhost",
  user: "your_username",
  password: "your_password",
  database: "radarDb",
});

服務器配置
服務器默認運行在端口 3000。
確保任何外部設備或服務都已配置與此端口上的服務器通信。
運行應用程序
開發模式
要啟動帶有熱重新加載的開發服務器：

npm run dev

在 http://localhost:3000 訪問應用程序。

生產模式
構建並啟動應用程序：
npm run build
npm start

使用
訪問儀表板：

在瀏覽器中導航到 http://localhost:3000。
實時數據流：

確保您的設備正在通過 /api/data 端點向服務器發送數據。
服務器接受帶有設備數據的 JSON 負載的 POST 請求。
數據可視化：

儀表板將在接收到新數據時自動更新。
互動式儀錶顯示電壓、電流、功率和累積功率的當前讀數。
API 端點
POST /api/data

接收來自設備的數據的端點。

期望以下格式的 JSON 負載：

{
  "data": [
    {
      "channel": 0,
      "type": "BATTERY_VOLTAGE",
      "value": 0
    },
    {
      "channel": 1,
      "type": "ELECTRIC_CURRENT",
      "value": 0
    }
  ]
}

GET /api/get-distance

從數據庫中獲取最新的距離數據。

返回 JSON 響應：
{
  "distance": 0
}

組件
Dashboard：使用儀錶圖顯示設備數據的主要組件。
BaseStation：可視化基站並模擬基於距離的功率調整。
樣式
全局樣式： 定義在 globals.css。

組件樣式：

dashboard.css：儀表板佈局和儀錶圖的樣式。
base-station.css：基站和汽車動畫的樣式。
資產
圖片： 存儲在 assets/images。
字體： 位於 fonts。
ESLint 配置
ESLint 已設置支持 Next.js 和 TypeScript。

配置文件：

.eslintrc.json
eslint.config.js
運行 ESLint：
npm run lint

TypeScript 配置
TypeScript 設置定義在 tsconfig.json 中。
使用別名進行路徑，以簡化導入。
依賴項
服務器端：

Express
Socket.IO
MySQL2
CORS
客戶端：

React
Next.js
Socket.IO Client
React Gauge Chart
Lodash
Chart.js
注意
如果從不同的源訪問服務器，請確保已正確配置 CORS。
該應用程序使用具有輪詢傳輸的 Socket.IO WebSocket，以提高兼容性。
故障排除
Socket 連接錯誤：

檢查服務器是否正在運行並可在正確的端口上訪問。
確認防火牆或網絡設置未阻止連接。
數據庫連接問題：

確認 MySQL 數據庫正在運行，並且憑據正確。
檢查是否存在 radartousrp 表並具有預期的結構。

授權
此項目使用 MIT 許可證。

