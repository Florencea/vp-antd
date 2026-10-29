# 未來探索與發想備忘錄（Future Explorations & Ideas）

本文檔記錄專案長遠發展與社群運營的**探索性發想**。目前僅作為思路沉澱與架構儲備，暫不進入具體工程實作，留待後續討論與定案。

---

## 發想一：GitHub Pages 組件官網與一鍵複製（Showcase & Copy-Paste Registry）

### 1. 核心發想

如同 `shadcn-ui` 徹底改變現代前端組件生態一般，使用者不再需要安裝笨重的黑盒 NPM 套件，而是直接在線上官網瀏覽組件：

- **動態 Theme 即時調節器**：首頁提供 Ant Design 經典色彩調節板（藍、綠、紫、橙、暗色模式），拉動色盤時，畫面上所有組件以 CSS `color-mix()` 實時響應，向開發者證明這套 Token 系統的和諧性。
- **高保真互動 Playground**：每個組件頁面提供互動式預覽（各變體、尺寸、狀態）。
- **一鍵複製源碼（One-Click Copy）**：
  - 介面上提供「Copy Code」按鈕，點擊直接複製該組件的純 Tailwind v4 + React Aria 原始碼。
  - 探索未來是否支援類似 CLI 註冊表（Registry JSON），讓使用者可透過 `vp add button` 或自定義命令直接將代碼拉入其專案。

### 2. 潛在技術架構

- 路由架構：直接利用專案現有的 TanStack Router 檔案路由（`src/routes/docs/` 或 `src/routes/components/`）。
- 代碼高亮：採用 Shiki 或 Prism 進行服務端/構建期代碼染色。
- 自動化部署：透過 `.github/workflows/deploy-pages.yml`，在 `push: main` 且通過全部測試後，將 `dist/` 一鍵部署至 GitHub Pages。

---

## 發想二：上游 Ant Design 變更追蹤監控機制（Upstream Sync Watcher）

### 1. 核心發想

為了解決傳統 UI 庫復刻專案隨著時間推移而「與官方官方脫節、無人維護」的宿命，建立一個**自動化上游變更雷達**：

- 當官方 Ant Design（`antd`）在 NPM 發布新版本時，自動獲取通知。
- 自動比對是否有：
  - 新發布的官方組件（提醒我們在 `docs/COMPONENTS_MATRIX.md` 中擴充）。
  - 官方 Token 結構調整（例如新增了某個語義 Map Token）。
  - 官方外觀或微動效的重大變更（如邊框色調、焦點陰影演進）。

### 2. 潛在實作思路

1. **輕量偵測腳本（`scripts/check-upstream-antd.ts`）**：
   - 透過 NPM Registry API（`https://registry.npmjs.org/antd/latest`）取得目前最新的 Antd 版本號與發布時間。
   - 抓取 Antd 的型別定義或 export 清單，與 `docs/COMPONENTS_MATRIX.md` 中的組件清單進行差集運算（Diff）。
2. **GitHub Actions 定時排程（Cron Workflow）**：
   - 每週一定時觸發工作流。
   - 若偵測到新版本或新組件，自動建立一則 GitHub Issue（例如：`[Upstream] Ant Design v6.x.x released with new component FloatButton`），並附上變更比對報告，提醒維護者安排 Agent 任務推進。

---

## 3. 下一步討論議題備忘

- [ ] 展示站的代碼複製型態：純前端剪貼簿複製 vs. 建立簡易 JSON Registry？
- [ ] 上游偵測腳本的比對粒度：僅比對組件名稱，還是連同 Token 變更一併透過 AST 分析比對？
- [ ] 官方發布暗黑模式演進時，如何自動同步色階調整？
