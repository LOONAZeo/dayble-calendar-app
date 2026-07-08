# Dayble 行事曆

簡潔可愛的中英雙語行事曆 PWA。單一 HTML 檔、離線可用、資料存在本機。

![icon](icons/icon-192.png)

## 功能

### 行事曆
- **四種檢視**：週 / 日 / 月 / 議程 (agenda)
- **事件管理**：標題、日期、起訖時間、分類、重複（每天／工作日／每週／每月）、提醒、備註
- **拖曳**移動事件與拉伸改時間、現在時間紅線、今天標記
- **5 個彩色分類**、待辦清單、台灣節日、全文搜尋

### 新功能
- **推播提醒**：瀏覽器 Notification API，每分鐘自動檢查，側欄按鈕授權
- **6 種主題**：粉紅 / 紫羅蘭 / 天藍 / 薄荷 / 珊瑚 / 深色，即時切換
- **上一步 / 下一步**：`Ctrl+Z` 復原、`Ctrl+Y` 重做，最多 20 步；桌面版 header 也有按鈕
- **時間智能跟隨**：修改開始時間時結束時間自動維持相同時長

### 基礎
- **本機儲存**（localStorage）＋ 跨分頁即時同步
- **手機 RWD**：FAB、側欄抽屜、底部導覽列
- **PWA**：「加到主畫面」變全螢幕 app、Service Worker 離線可用

## 本機執行

Service Worker 需要 HTTP 伺服器（直接雙擊 `file://` 會讓 SW 失效）：

```bash
python -m http.server 8080
```

開啟 <http://localhost:8080>

## 部署到 GitHub Pages

1. 推到 GitHub repo
2. repo → **Settings → Pages** → Source 選 `Deploy from a branch`，branch 選 `master`，資料夾 `/(root)`
3. 幾分鐘後即可用 `https://loonazeo.github.io/dayble-calendar-app/` 開啟
4. 手機瀏覽器開網址 → 選單 → **加到主畫面**

## 包成原生 App（Capacitor）

同一份網頁可用 [Capacitor](https://capacitorjs.com/) 包成 Android / iOS 原生 app：

```bash
npm init -y
npm i @capacitor/core @capacitor/cli @capacitor/local-notifications
npx cap init Dayble app.dayble.calendar --web-dir .
npx cap add android   # 需要 Android Studio
npx cap copy
npx cap open android
```

## 技術說明

| 檔案 | 說明 |
|------|------|
| `index.html` | App 本體（React.createElement 撰寫，DCLogic 元件框架） |
| `runtime.js` | React 18 + dc 框架執行環境 |
| `sw.js` | Service Worker，快取離線資源 |
| `manifest.webmanifest` | PWA 安裝設定 |
| `icons/` | 小金毛 + 馬爾濟斯自製圖示，各尺寸 |

## Roadmap

- [ ] 資料匯出／匯入 JSON 備份
- [ ] 自訂分類（新增／改色／刪除）
- [ ] 週／日檢視同時段事件並排排版
- [ ] 節日改為可訂閱（.ics）
- [ ] Capacitor 包裝成 App Store / Play Store 上架

## License

MIT — 見 [LICENSE](LICENSE)
