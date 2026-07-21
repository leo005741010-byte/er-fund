# 天晟急診科基金

急診科基金收支管理，單檔網頁 App（HTML + Firebase Realtime Database），可安裝到手機當 App 用。

## 功能

- **每月入帳**：逐月登錄科基金撥款金額與備註
- **支出登錄**：日期、用途、分類、金額、**代墊者**、備註、填表人
- **請款狀態三段**：未請款 → 已請款待撥 → **已付款**（代墊者已實際拿到錢）
- **請款結算**：依代墊者彙總待付金額，可整批標記已請款／已付款
- **總覽**：累計結餘、當月收支、待付給代墊者總額
- **統計**：每月收支、分類佔比、各人代墊統計
- **匯出**：CSV（Excel 可直接開）、JSON 備份／還原
- **全站密碼**：輸入密碼才能看到資料
- **雲端同步**：所有裝置即時共用同一份資料
- **離線可用**：Service Worker 快取，沒網路也開得起來

## 檔案

| 檔案 | 說明 |
|---|---|
| `index.html` | 整個 App（HTML/CSS/JS 全部內嵌） |
| `manifest.json` | PWA 安裝設定 |
| `sw.js` | Service Worker（離線快取） |
| `icon-*.png` | App 圖示 |

## 資料存放

- 雲端：Firebase Realtime Database，路徑 `erFundData`
- 本機：`localStorage` key `tienSheng_erFund_v1`（離線備援）

寫入採子節點更新（`expenses/<id>`、`income/<月份>`），多人同時編輯不會互相覆蓋。

**成員姓名不寫在原始碼裡**，只存在雲端資料庫，請在 App 的「設定 → 成員」新增。

## 部署

推到 GitHub 後於 repo Settings → Pages 選 `main` branch / root 即可。
改版後執行 `更新科基金網站.bat` 一鍵 commit + push。
