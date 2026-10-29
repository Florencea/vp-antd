# Ant Design Reborn 架構白皮書

## 1. 願景與背景（Vision & Background）

`vp-antd` 最初誕生於解決 Ant Design 與 Tailwind CSS 樣式隔離與特異度衝突的痛點。然而隨著前端架構發展與實踐，傳統 Ant Design 在現代 Web 生態中逐漸顯現出深層的結構性瓶頸：

- **可訪問性（a11y）受限**：過度嵌套的黑盒 DOM、合成事件機制與非標準屬性，難以完整符合 W3C WAI-ARIA 1.2 規範。
- **國際化（i18n）與原生標準脫節**：依賴中央單例 `ConfigProvider` 與 `Dayjs` 綁定，無法輕易善用現代瀏覽器原生的 `Intl` 生態（複數規則、多曆法、時區算術與雙向文字 RTL）。
- **AI Agent（智慧體協同）摩擦**：Antd 的「黑盒封裝 + 龐大專屬 props + 動態 CSS-in-JS 哈希」對 LLM 而言是極難直觀推導與修改的暗箱，極易產出不合規的屬性組合或引發特異度衝突。
- **React 19 與現代底層斷層**：現代生態全面轉向原生 Form Actions、`useActionState`、`useOptimistic` 與 Direct Ref，Antd 內部龐大的 `rc-*` 狀態機已無法享受最新底層演進的完全紅利。

**Ant Design Reborn 的核心使命**：

> **「在外觀、質感、微動效與色彩體系上，1:1 精準復刻 Ant Design v6；在內核、架構與開發者體驗上，徹底轉向現代標準（Tailwind CSS v4 `@theme` 設計系統、React Aria Components 無障礙原語、TanStack Form/Table 與 React 19 原生能力）。」**

---

## 2. 核心架構原則（Core Principles）

### 2.1 零運行時 Token 體系（Tailwind CSS v4 `@theme`）

Ant Design v6 最強大的是其基於 Seed Tokens 衍生 Map Tokens 的數學關聯算法（修改 `colorPrimary`，按鈕 Hover、Active、淺色底色、外邊框與 Focus 光暈自動以固定比例協同調整）。

我們摒棄 CSS-in-JS 運行時開銷，利用現代 CSS 的原生 `color-mix(in srgb, ...)` 與 Tailwind v4 `@theme`，在 **純 CSS 層** 實現這套完整的衍生矩陣：

- **Seed Tokens**：定義核心種子變數（`--color-primary-base`, `--radius-base`, `--control-height`）。
- **Map Tokens**：透過 `color-mix()` 自動按嚴格比例計算衍生色階。
- **全域協同調整**：只需在根層級微調一個 CSS 變數，整個應用所有組件的階調、光暈、陰影與圓角自動重算，保持和諧，無任何視覺撕裂。

### 2.2 不復刻黑盒 API，擁抱現代生態標準

- **不再使用 Antd 的專屬黑盒 Props**（如 `columns` 配置物件、`Form.useForm` 閉包實例）。
- **標準 Headless 原語貫通**：
  - **表單**：採用 `@tanstack/react-form` + Zod，完美支援 React 19 Server Actions、`useActionState` 與原生表單提交。
  - **表格**：採用 `@tanstack/react-table` 標準 headless API，提供完整排序、過濾、分頁與虛擬滾動能力。
  - **彈窗與覆蓋層**：採用 `react-aria-components` 的宣告式 JSX 與焦點管理。
  - **國際化**：採用 `@internationalized/date`，完全基於瀏覽器原生 `Intl` API。

### 2.3 開放源碼與 Agent 友善（Open-Code & Agent-Ready）

- 組件以源碼形式存在於專案的 `src/components/ui/` 目錄中（Open-code pattern）。
- 採用標準 React 19 原生屬性透傳（直傳 `ref`、`className`、`children`）。
- AI Agent 能 100% 直觀讀取與編輯每一行語義化 HTML 標籤與 Tailwind 樣式，不再需要猜測黑盒邏輯。

---

## 3. 設計系統 Token 規範（Design Tokens Specification）

### 3.1 色彩階調層次（Color Palette）

```css
@theme {
  /* Seed Tokens */
  --color-primary-base: #1677ff;
  --color-success-base: #52c41a;
  --color-warning-base: #faad14;
  --color-error-base: #ff4d4f;
  --color-info-base: #1677ff;

  --color-text-base: #000000;
  --color-bg-base: #ffffff;

  /* Map Tokens: 衍生色階 */
  --color-primary: var(--color-primary-base);
  --color-primary-hover: color-mix(in srgb, var(--color-primary-base) 80%, white);
  --color-primary-active: color-mix(in srgb, var(--color-primary-base) 82%, black);
  --color-primary-bg: color-mix(in srgb, var(--color-primary-base) 6%, white);
  --color-primary-border: color-mix(in srgb, var(--color-primary-base) 35%, white);
  --color-primary-outline: color-mix(in srgb, var(--color-primary-base) 18%, transparent);

  /* 文字四級層次 (Ant Design 經典 Alpha 階調) */
  --color-text-title: rgba(0, 0, 0, 0.88);
  --color-text-body: rgba(0, 0, 0, 0.88);
  --color-text-secondary: rgba(0, 0, 0, 0.65);
  --color-text-tertiary: rgba(0, 0, 0, 0.45);
  --color-text-quaternary: rgba(0, 0, 0, 0.25);

  /* 容器與表面 */
  --color-border: #d9d9d9;
  --color-border-secondary: #f0f0f0;
  --color-bg-container: #ffffff;
  --color-bg-layout: #f5f5f5;
  --color-bg-elevated: #ffffff;

  /* 尺寸與圓角 */
  --radius-base: 8px;
  --radius-sm: 4px;
  --radius-md: var(--radius-base);
  --radius-lg: 12px;
  --control-height: 32px;
}
```

### 3.2 標誌性 Antd 微動效（Micro-Animations）

- **Button 水波紋（Wave Animation）**：
  ```css
  @keyframes antd-wave-spread {
    0% {
      box-shadow: 0 0 0 0px var(--wave-color, var(--color-primary));
      opacity: 0.8;
    }
    100% {
      box-shadow: 0 0 0 6px var(--wave-color, var(--color-primary));
      opacity: 0;
    }
  }

  .ant-btn-wave:active::after {
    content: "";
    position: absolute;
    inset: -1px;
    border-radius: inherit;
    animation: antd-wave-spread 0.4s cubic-bezier(0.08, 0.82, 0.17, 1);
    pointer-events: none;
  }
  ```
- **彈窗縮放淡入（Modal Scale-In）**：
  彈出時由 80% 放大至 100% 並伴隨淡入；關閉時平滑淡出縮小。

---

## 4. 與全端專案 `vp-hono` 的差異化定位

| 維度         | `vp-hono`                                                                     | `vp-antd` (Ant Design Reborn)                                     |
| :----------- | :---------------------------------------------------------------------------- | :---------------------------------------------------------------- |
| **核心定位** | 全端單體架構範本（Full-Stack Monolith）                                       | 純前端無障礙企業級設計系統與復刻庫（Design System & UI Kit）      |
| **核心強項** | 端到端型別安全（RPC、Drizzle ORM、OpenAPI）                                   | 極致高保真視覺復刻、Tailwind v4 Token 體系、全 65+ 組件無障礙覆蓋 |
| **設計風格** | 偏向通用 shadcn-ui 現代簡約風                                                 | 嚴格 1:1 復刻 Ant Design 經典商務高密度排版與微動效               |
| **協同關係** | 未來 `vp-hono` 若需要建構 Antd 風格的企業後台，可直接無縫引用本專案的組件代碼 |
