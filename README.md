# 天晟急診科基金

急診科基金收支管理，單檔網頁 App（HTML + Firebase Realtime Database），可安裝到手機當 App 用。

## 功能

- **每月入帳**：逐月登錄科基金撥款金額與備註
- **支出登錄**：日期、用途、分類、金額、**代墊者**、備註、填表人；日期不可填未來
- **發票照片**：拍照或選相簿，自動壓縮（長邊 1400px、約 50KB）後存雲端
- **狀態兩段**：<code>請款中</code> → <code>已到帳</code>（代墊者已實際拿到錢）
- **簽名確認**：切到「已到帳」時必須由代墊者手寫簽名，簽名圖留存為收款憑證；可一次簽多筆共用一張簽名
- **請款結算**：依代墊者彙總還沒拿到的金額，一鍵簽收結清
- **總覽**：累計結餘、當月收支、代墊者還沒拿到的總額
- **統計**：每月收支、分類佔比、各人代墊統計
- **匯出**：CSV（Excel 可直接開）、JSON 備份／還原
- **雲端同步**：所有裝置即時共用同一份資料
- **離線可用**：Service Worker 快取，沒網路也開得起來（照片／簽名需連線）

## 檔案

| 檔案 | 說明 |
|---|---|
| `index.html` | 整個 App（HTML/CSS/JS 全部內嵌） |
| `操作說明.html` | 使用手冊 |
| `manifest.json` | PWA 安裝設定 |
| `sw.js` | Service Worker（離線快取） |
| `icon-*.png` | App 圖示 |

## 資料存放

| 路徑 | 內容 | 同步方式 |
|---|---|---|
| `erFundData` | 帳目（expenses / income / members / cats / opening） | 即時監聽 |
| `erFundFiles` | `photo/<支出id>`、`sig/<簽名id>` | 需要時才抓 |

照片和簽名刻意存在另一支 ref，帳目即時同步時不會被大檔案拖慢。
本機另存 `localStorage` key `tienSheng_erFund_v1` 作離線備援（不含照片）。

寫入採子節點更新（`expenses/<id>`、`income/<月份>`），多人同時編輯不會互相覆蓋。

**沒有密碼保護**，知道網址就看得到。**成員姓名不寫在原始碼裡**，只存在雲端資料庫，請在 App 的「設定 → 成員」新增。

## 部署

推到 GitHub 後於 repo Settings → Pages 選 `main` branch / root 即可。
改版後執行 `更新科基金網站.bat` 一鍵 commit + push。
