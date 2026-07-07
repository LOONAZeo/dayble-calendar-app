# Dayble 行事曆 📅

簡潔可愛的中英雙語行事曆 PWA。單一 HTML 檔、離線可用、資料存在本機。

![view](icons/icon-192.png)

## 功能

- **四種檢視**：週 / 日 / 月 / 議程 (agenda)
- **事件**：標題、日期、起訖時間、分類、重複（每天／工作日／每週／每月）、提醒、備註
- **拖曳**移動與拉伸改時間、現在時間紅線、今天標記
- **5 個彩色分類**、待辦清單、台灣節日、搜尋
- **本機儲存**（localStorage）＋ 跨分頁同步
- **手機 RWD**：FAB、側欄、底部導覽
- **PWA**：可「加到主畫面」變全螢幕 app、離線可用

## 本機執行

因為用了 Service Worker 與 `fetch`，需要用 HTTP 伺服器開啟（直接雙擊 `file://` 會讓 SW 失效）：

```bash
# 擇一
python -m http.server 8080
npx serve .
```

然後開 <http://localhost:8080>。

## 部署到 GitHub Pages

1. 推到 GitHub。
2. repo → **Settings → Pages** → Source 選 `Deploy from a branch`，branch 選 `main` / 資料夾 `/ (root)`。
3. 幾分鐘後即可用 `https://<你的帳號>.github.io/dayble-calendar/` 開啟。
4. 手機瀏覽器開該網址 → 分享／選單 → **加到主畫面**。

## 之後包成手機商店 App（Capacitor）

同一份網頁可用 [Capacitor](https://capacitorjs.com/) 包成 Android / iOS 原生 app，並取得真正的本地通知：

```bash
npm init -y
npm i @capacitor/core @capacitor/cli @capacitor/local-notifications
npx cap init Dayble app.dayble.calendar --web-dir .
npx cap add android   # 需要 Android Studio
npx cap copy
npx cap open android
```

## 技術說明

- `index.html`：app 本體（UI 以 `React.createElement` 撰寫，掛在 `<x-dc>` 模板槽上）。
- `runtime.js`：內含 React 18 + dc 元件框架的執行環境（自 Claude Artifact 匯出，已從原本 6MB 內嵌字型瘦身為 Google Fonts 連結）。
- `sw.js` / `manifest.webmanifest`：PWA 離線與安裝設定。

## Roadmap

- [ ] 提醒真正發出通知（Notifications API + SW；手機用 Capacitor local notifications）
- [ ] 資料匯出／匯入 JSON 備份
- [ ] 自訂分類（新增／改色／刪除）
- [ ] 週／日檢視同時段事件並排排版
- [ ] 深色模式
- [ ] 節日改為可計算／可訂閱（.ics）

## License

MIT — 見 [LICENSE](LICENSE)。
