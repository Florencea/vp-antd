# 組件開發與編寫規範指南（Component Authoring Guide）

本文檔為人類開發者與 AI Agent 開發新組件時的**強制規範與實作檢查清單**。所有組件必須嚴格遵守以下範式，以確保設計系統協調性、無障礙達標率與代碼透明度。

---

## 1. 檔案拓撲與命名準則

- **放置路徑**：所有復刻組件一律置於 `src/components/ui/` 目錄下。
- **命名規範**：
  - 單一檔案組件使用短橫線（kebab-case），如 `src/components/ui/button.tsx`、`src/components/ui/date-picker.tsx`。
  - 具備複合子組件的複雜模組可建立專屬子目錄，如 `src/components/ui/table/` 或 `src/components/ui/form/`。
- **工具庫與變體管理**：
  - 統一使用 `class-variance-authority` (cva) 定義樣式變體。
  - 統一使用 `src/lib/utils.ts` 中的 `cn(...)`（結合 `clsx` 與 `tailwind-merge`）合併類名。

---

## 2. 設計系統與樣式規範（Design Token Rules）

### 2.1 嚴禁硬編碼顏色

- ❌ **絕對禁止**：`bg-[#1677ff]`, `text-[#ff4d4f]`, `border-[#d9d9d9]`, `style={{ color: 'red' }}`。
- ✅ **必須使用語義化 Token**：
  - 主色系：`bg-primary`, `hover:bg-primary-hover`, `active:bg-primary-active`, `border-primary`, `bg-primary-bg`
  - 狀態色：`text-success`, `text-warning`, `text-error`, `bg-error-bg`
  - 容器與邊框：`bg-container`, `bg-layout`, `border-border`, `border-border-secondary`
  - 文字層次：`text-text-title`, `text-text-body`, `text-text-secondary`, `text-text-tertiary`

### 2.2 圓角與尺寸規格

- 控件高度：預設高度使用 `h-control`（32px）、小尺寸 `h-6`（24px）、大尺寸 `h-10`（40px）。
- 圓角：小圓角 `rounded-sm`（4px）、預設圓角 `rounded-md`（8px）、大圓角 `rounded-lg`（12px）。

---

## 3. 標誌性 Ant Design 微動效實作規範

### 3.1 Button 水波紋（Wave Animation）

按鈕組件必須具備 `.ant-btn-wave` 類名，當滑鼠點擊釋放或鍵盤觸發時，由 `:active::after` 觸發 CSS keyframe 水波擴散動畫：

```tsx
// 變體基類必須包含 ant-btn-wave
const buttonVariants = cva(
  "relative inline-flex items-center justify-center font-normal transition-all outline-none ant-btn-wave select-none disabled:cursor-not-allowed disabled:opacity-50",
  // ...
);
```

### 3.2 Focus 光暈效果（Halo Outline）

表單輸入類組件（Input, Select, DatePicker, Checkbox）在獲取焦點時，必須具備 Antd 標誌性的外散發光效果：

```css
focus: border-primary focus: shadow-[0_0_0_2px_var(--color-primary-outline)];
```

### 3.3 彈窗中心縮放動效（Scale-In）

Dialog / Modal 在開啟與關閉時，必須使用縮放動畫：

```css
data-[entering]: animate-in data-[entering]: fade-in-0 data-[entering]: zoom-in-95
  data-[exiting]: animate-out data-[exiting]: fade-out-0 data-[exiting]: zoom-out-95;
```

---

## 4. 可訪問性（a11y）強制檢查表

每個組件在交付前必須滿足以下 WAI-ARIA 1.2 標準：

- [ ] **鍵盤可操作性**：組件所有功能均可純透過 `Tab`、`Shift + Tab`、`Enter`、`Space`、`Arrow` 鍵完整操作。
- [ ] **焦點管理**：彈窗（Modal / Drawer）必須鎖定焦點在容器內（Focus Trap），關閉後焦點必須自動歸還至原始觸發按鈕。
- [ ] **ARIA 狀態綁定**：開關/選取類具備 `aria-checked` 或 `aria-selected`；展開類具備 `aria-expanded` 與 `aria-controls`。
- [ ] **螢幕閱讀器友善**：圖標按鈕必須提供 `aria-label`；表單輸入欄位必須關聯 `aria-labelledby` 或 `aria-describedby` 錯誤訊息。

---

## 5. 標準組件代碼樣板（Template）

以下為典型組件（以 `Button` 為例）的標準結構：

```tsx
import { Button as AriaButton, type ButtonProps as AriaButtonProps } from "react-aria-components";
import { cva, type VariantProps } from "class-variance-authority";
import { cn } from "../../lib/utils";

const buttonVariants = cva(
  "relative inline-flex items-center justify-center font-normal transition-all outline-none ant-btn-wave select-none disabled:cursor-not-allowed disabled:opacity-50",
  {
    variants: {
      variant: {
        primary:
          "bg-primary text-white hover:bg-primary-hover active:bg-primary-active border border-primary shadow-xs",
        default:
          "bg-container text-text-body border border-border hover:border-primary hover:text-primary active:border-primary-active shadow-xs",
        dashed:
          "bg-container text-text-body border border-dashed border-border hover:border-primary hover:text-primary active:border-primary-active",
        text: "bg-transparent text-text-body hover:bg-black/5 active:bg-black/10 border-transparent",
        link: "bg-transparent text-primary hover:text-primary-hover active:text-primary-active border-transparent p-0 h-auto",
      },
      size: {
        small: "h-6 px-2 text-xs rounded-sm",
        middle: "h-control px-3.75 text-sm rounded-md",
        large: "h-10 px-4 text-base rounded-lg",
      },
      danger: {
        true: "",
      },
    },
    compoundVariants: [
      {
        variant: "primary",
        danger: true,
        className:
          "bg-error border-error hover:bg-error/80 active:bg-error/90 [--wave-color:var(--color-error)]",
      },
      {
        variant: "default",
        danger: true,
        className: "text-error border-error hover:border-error hover:text-error/80",
      },
    ],
    defaultVariants: {
      variant: "default",
      size: "middle",
    },
  },
);

export interface ButtonProps extends AriaButtonProps, VariantProps<typeof buttonVariants> {
  className?: string;
  loading?: boolean;
}

export function Button({
  variant,
  size,
  danger,
  loading,
  className,
  children,
  ...props
}: ButtonProps) {
  return (
    <AriaButton
      isDisabled={props.isDisabled || loading}
      className={cn(buttonVariants({ variant, size, danger }), className)}
      {...props}
    >
      {loading && <span className="mr-1.5 animate-spin">⏳</span>}
      {children}
    </AriaButton>
  );
}
```

---

## 6. 單元測試驗證規範（Vitest Browser Playwright）

每個組件完成後，必須在 `test/` 目錄建立相應的測試（例如 `test/button.test.tsx`），執行真實 Chromium 渲染測試：

1. **渲染與尺寸斷言**：驗證預設高度、邊框顏色符合 Token 計算值。
2. **互動與狀態斷言**：點擊觸發事件、Disabled 狀態不可點擊。
3. **無障礙斷言**：測試焦點移入與按鍵 Enter / Space 觸發行為。
