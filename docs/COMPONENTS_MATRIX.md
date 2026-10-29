# Ant Design Reborn 全組件追蹤矩陣（Components Parity Matrix）

本文檔追蹤 Ant Design 全部組件（約 65 個）在現代架構下的復刻狀態、底層技術選型與優先級。

> **狀態標記說明**：
>
> - ⬜ **未開始（Todo）**
> - 🟡 **進行中（In Progress）**
> - ✅ **已完成（Completed）**

---

## 1. 通用組件（General）

| 組件名稱        | Ant Design 對標 | 底層技術選型                       | 狀態 | 優先級 | 核心特性與動效                                                                               |
| :-------------- | :-------------- | :--------------------------------- | :--: | :----: | :------------------------------------------------------------------------------------------- |
| **Button**      | `Button`        | `react-aria-components` Button     |  ⬜  |   P0   | 點擊擴散水波紋（Wave Animation）、Primary/Default/Dashed/Text/Link 變體、Danger 態、加載狀態 |
| **FloatButton** | `FloatButton`   | 原生 Fixed 容器 + Button           |  ⬜  |   P2   | 頁面右下角懸浮按鈕、BackTop 回到頂部、Group 展開菜單                                         |
| **Icon**        | `Icon`          | `lucide-react` 封裝                |  ⬜  |   P0   | 語意化圖標、相容 Antd 常用圖標尺寸與色彩                                                     |
| **Typography**  | `Typography`    | React 19 原生 HTML 標籤 + Tailwind |  ⬜  |   P0   | Title (H1-H5)、Text (secondary/success/warning/danger/code)、Paragraph (展開/收合)           |

---

## 2. 佈局組件（Layout）

| 組件名稱    | Ant Design 對標                                  | 底層技術選型                | 狀態 | 優先級 | 核心特性與動效                                             |
| :---------- | :----------------------------------------------- | :-------------------------- | :--: | :----: | :--------------------------------------------------------- |
| **Divider** | `Divider`                                        | 語義化 `<hr>` 或 `<div>`    |  ⬜  |   P0   | 實線/虛線、水平/垂直、標題文字置左/置中/置右               |
| **Flex**    | `Flex`                                           | Tailwind Flex 工具類        |  ⬜  |   P0   | 彈性佈局容器、Gap、Wrap、Align、Justify                    |
| **Grid**    | `Row`, `Col`                                     | Tailwind 24 柵格系統        |  ⬜  |   P1   | 24 欄響應式佈局、Gutter 間距、Flex 偏移與對齊              |
| **Layout**  | `Layout`, `Header`, `Sider`, `Content`, `Footer` | 語義化 HTML 佈局容器        |  ⬜  |   P1   | 經典後台佈局骨架、Sider 可收合側邊欄（響應式斷點與微動效） |
| **Space**   | `Space`                                          | Tailwind Flex / Inline-flex |  ⬜  |   P1   | 組件間距自動填充、垂直/水平排版、分組間隔線                |

---

## 3. 導航組件（Navigation）

| 組件名稱       | Ant Design 對標 | 底層技術選型                           | 狀態 | 優先級 | 核心特性與動效                                                         |
| :------------- | :-------------- | :------------------------------------- | :--: | :----: | :--------------------------------------------------------------------- |
| **Breadcrumb** | `Breadcrumb`    | `react-aria-components` Breadcrumbs    |  ⬜  |   P1   | 路徑導航、分隔符自訂、整合 TanStack Router `Link`                      |
| **Dropdown**   | `Dropdown`      | `react-aria-components` Menu + Popover |  ⬜  |   P1   | 觸發式下拉選單、分割按鈕（Dropdown.Button）、淡入淡出微動效            |
| **Menu**       | `Menu`          | `react-aria-components` Menu           |  ⬜  |   P1   | 垂直/水平/內嵌菜單、選中高亮背景、可折疊子菜單                         |
| **Pagination** | `Pagination`    | 獨立分頁原語 / TanStack Table          |  ⬜  |   P0   | 頁碼按鈕組、前後翻頁、快速跳轉輸入框、每頁筆數下拉（PageSize Changer） |
| **Steps**      | `Steps`         | 現代 SVG / Flex 連線步驟條             |  ⬜  |   P2   | 水平/垂直步驟條、成功/處理中/等待中/錯誤狀態圖標、點狀步驟條           |
| **Tabs**       | `Tabs`          | `react-aria-components` Tabs           |  ⬜  |   P0   | 底部滑動藍條指示器（Slide-bar）、卡片模式、可關閉標籤（Editable-card） |

---

## 4. 數據錄入（Data Entry）

| 組件名稱         | Ant Design 對標               | 底層技術選型                                        | 狀態 | 優先級 | 核心特性與動效                                                      |
| :--------------- | :---------------------------- | :-------------------------------------------------- | :--: | :----: | :------------------------------------------------------------------ |
| **AutoComplete** | `AutoComplete`                | `react-aria-components` ComboBox                    |  ⬜  |   P2   | 自動完成輸入框、即時過濾下拉推薦                                    |
| **Cascader**     | `Cascader`                    | 級聯 Popover 組合                                   |  ⬜  |   P2   | 多層級聯選擇器、動態加載次級選單                                    |
| **Checkbox**     | `Checkbox`, `Checkbox.Group`  | `react-aria-components` Checkbox                    |  ⬜  |   P0   | 方框選中動效、半選態（Indeterminate）、群組佈局                     |
| **ColorPicker**  | `ColorPicker`                 | 原生 HTML5 Color / React Aria                       |  ⬜  |   P3   | 顏色選取面板、預設調色盤                                            |
| **DatePicker**   | `DatePicker`, `RangePicker`   | `react-aria-components` + `@internationalized/date` |  ⬜  |   P0   | 經典 Antd 單雙欄日曆面板、快捷區、雙向文字與原生 Intl 時區計算      |
| **Form**         | `Form`, `Form.Item`           | `@tanstack/react-form` + Zod                        |  ⬜  |   P0   | 支援 React 19 Actions、垂直/水平排版、必填星號、錯誤滑動提示        |
| **Input**        | `Input`, `TextArea`, `Search` | `react-aria-components` TextField                   |  ⬜  |   P0   | Focus 藍色外光暈（Box-shadow Halo）、前後綴、一鍵清除按鈕、字數統計 |
| **InputNumber**  | `InputNumber`                 | `react-aria-components` NumberField                 |  ⬜  |   P1   | 步進器小按鈕、格式化金額/百分比、範圍限定                           |
| **Mentions**     | `Mentions`                    | 提及觸發輸入框                                      |  ⬜  |   P3   | `@` 提及關鍵字下拉選單                                              |
| **Radio**        | `Radio`, `Radio.Group`        | `react-aria-components` RadioGroup                  |  ⬜  |   P0   | 經典圓點選中動效、按鈕樣式單選（Radio.Button）                      |
| **Rate**         | `Rate`                        | `react-aria-components` Slider 或自訂               |  ⬜  |   P2   | 五角星評分、支援半星選取、自訂字元                                  |
| **Select**       | `Select`                      | `react-aria-components` Select                      |  ⬜  |   P0   | 單選/多選/標籤模式（Tags）、搜尋過濾、選中勾選符號、下拉滑動動效    |
| **Slider**       | `Slider`                      | `react-aria-components` Slider                      |  ⬜  |   P1   | 滑動輸入條、雙滑塊範圍選擇、刻度標記（Marks）                       |
| **Switch**       | `Switch`                      | `react-aria-components` Switch                      |  ⬜  |   P0   | 膠囊型滑塊動效、內部文字或圖標（開/關提示）                         |
| **TimePicker**   | `TimePicker`                  | `react-aria-components` TimeField                   |  ⬜  |   P1   | 時/分/秒滾動滾輪選擇器                                              |
| **Transfer**     | `Transfer`                    | 雙欄表格/穿梭盒                                     |  ⬜  |   P2   | 雙向穿梭框、全選/搜尋/自訂列                                        |
| **TreeSelect**   | `TreeSelect`                  | 樹形 Popover 結合                                   |  ⬜  |   P3   | 樹形結構下拉選擇器                                                  |
| **Upload**       | `Upload`                      | 原生 File Input + Dropzone                          |  ⬜  |   P1   | 點擊/拖曳上傳區域、檔案列表預覽、進度條顯示                         |

---

## 5. 數據展示（Data Display）

| 組件名稱         | Ant Design 對標               | 底層技術選型                       | 狀態 | 優先級 | 核心特性與動效                                                        |
| :--------------- | :---------------------------- | :--------------------------------- | :--: | :----: | :-------------------------------------------------------------------- |
| **Avatar**       | `Avatar`, `Avatar.Group`      | 現代 Image / Initials 封裝         |  ⬜  |   P1   | 圓形/方形頭像、文字縮放、疊加群組                                     |
| **Badge**        | `Badge`, `Ribbon`             | 純 Tailwind v4 樣式封裝            |  ⬜  |   P0   | 經典小紅點、數字徽標、狀態圓點（Processing 擴散波紋動畫）、緞帶徽章   |
| **Calendar**     | `Calendar`                    | `@internationalized/date` 月曆     |  ⬜  |   P2   | 完整月曆/年曆視圖、自訂日期單元格排程內容                             |
| **Card**         | `Card`, `Card.Grid`           | 語義化容器封裝                     |  ⬜  |   P0   | 經典邊框與圓角、標題欄操作區、封面圖、卡片網格                        |
| **Carousel**     | `Carousel`                    | 現代 CSS Scroll-Snap 或輕量輪播    |  ⬜  |   P2   | 平滑滑動輪播、指示點導航、自動播放                                    |
| **Collapse**     | `Collapse`                    | `react-aria-components` Disclosure |  ⬜  |   P1   | 經典手風琴折疊面板、旋轉箭頭圖示、無邊框模式                          |
| **Descriptions** | `Descriptions`                | 描述列表 (dl / dt / dd)            |  ⬜  |   P1   | 詳情資訊列表、帶邊框/無邊框表格化排版                                 |
| **Empty**        | `Empty`                       | SVG 向量圖 + 文字封裝              |  ⬜  |   P0   | 經典空狀態插圖、自訂描述與操作按鈕                                    |
| **Image**        | `Image`, `Image.PreviewGroup` | 原生 `<img>` + Modal 預覽          |  ⬜  |   P1   | 圖片預覽彈窗、縮放/旋轉/翻頁控制                                      |
| **List**         | `List`                        | 語義化 `<ul>` / `<li>` 列表        |  ⬜  |   P1   | 支援分頁與加載更多、自訂列表項前綴圖標與操作列                        |
| **Popover**      | `Popover`                     | `react-aria-components` Popover    |  ⬜  |   P1   | 氣泡浮層面板、帶標題與內容區、箭頭指示器                              |
| **QRCode**       | `QRCode`                      | 輕量 SVG QR Code 引擎              |  ⬜  |   P2   | 向量 QR Code 生成、中心帶 Logo、過期重刷遮罩                          |
| **Segmented**    | `Segmented`                   | `react-aria-components` RadioGroup |  ⬜  |   P1   | 現代分段控制器、背景平滑滑動高亮塊                                    |
| **Statistic**    | `Statistic`, `Countdown`      | 數字統計展示封裝                   |  ⬜  |   P1   | 數值統計、前後綴文字、倒數計時器                                      |
| **Table**        | `Table`                       | `@tanstack/react-table`            |  ⬜  |   P0   | 經典邊框、表頭排序小箭頭、多列固定、選取 Checkbox、與 Pagination 連動 |
| **Tag**          | `Tag`, `CheckableTag`         | 純 Tailwind v4 樣式封裝            |  ⬜  |   P0   | 經典 Preset 色彩（綠/藍/橘/紅/灰）、可關閉（Closeable）、可選中標籤   |
| **Timeline**     | `Timeline`                    | 垂直節點連線佈局                   |  ⬜  |   P1   | 時間軸節點、不同顏色圓點、幽靈節點（Pending）                         |
| **Tooltip**      | `Tooltip`                     | `react-aria-components` Tooltip    |  ⬜  |   P0   | 黑色經典小字浮層、箭頭定位、延遲觸發                                  |
| **Tour**         | `Tour`                        | 引導遮罩與高亮定位                 |  ⬜  |   P3   | 漫遊式新功能引導步驟泡泡                                              |
| **Tree**         | `Tree`                        | 遞迴列表組件                       |  ⬜  |   P2   | 樹形控件、展開/折疊節點、複選框選取、拖曳排序                         |

---

## 6. 反饋組件（Feedback）

| 組件名稱         | Ant Design 對標 | 底層技術選型                          | 狀態 | 優先級 | 核心特性與動效                                                   |
| :--------------- | :-------------- | :------------------------------------ | :--: | :----: | :--------------------------------------------------------------- |
| **Alert**        | `Alert`         | 警告提示條容器                        |  ⬜  |   P0   | 四色警告（Success/Info/Warning/Error）、帶圖標、輔助描述、可關閉 |
| **Drawer**       | `Drawer`        | `react-aria-components` ModalOverlay  |  ⬜  |   P0   | 左右上下四向平滑抽屜滑入、遮罩模糊、右上關閉鈕                   |
| **Message**      | `message`       | 頂部 Toast 容器 (如 Sonner 封裝)      |  ⬜  |   P0   | 頁面中上方滑入滑出提示、成功/警告/錯誤圖標、自動消失倒數         |
| **Modal**        | `Modal`         | `react-aria-components` Dialog        |  ⬜  |   P0   | 中心彈出縮放淡入、遮罩淡入、自帶 Confirm 確認對話框與雙按鈕佈局  |
| **Notification** | `notification`  | 邊角懸浮通知容器                      |  ⬜  |   P1   | 頁面四角彈出通知卡片、帶標題/描述與按鈕操作                      |
| **Popconfirm**   | `Popconfirm`    | `react-aria-components` DialogTrigger |  ⬜  |   P0   | 氣泡確認框、確認/取消雙按鈕、確認後回調                          |
| **Progress**     | `Progress`      | 圓環 / 橫條 SVG 進度條                |  ⬜  |   P1   | 經典藍色進度條、動態成功勾選動效、儀表盤樣式                     |
| **Result**       | `Result`        | 結果反饋頁面佈局                      |  ⬜  |   P1   | 403 / 404 / 500 / 成功 / 警告結果插圖與主副操作按鈕              |
| **Skeleton**     | `Skeleton`      | Tailwind 骨架屏封裝                   |  ⬜  |   P1   | 經典骨架卡片、頭像、標題與段落流光閃爍動畫                       |
| **Spin**         | `Spin`          | SVG 旋轉加載菊花                      |  ⬜  |   P0   | 經典四色花瓣旋轉圖標、全區域遮罩 Loading 容器                    |
| **Watermark**    | `Watermark`     | Canvas 動態生成浮水印背景             |  ⬜  |   P2   | 頁面或局部區域防篡改防刪除文字/圖片浮水印                        |

---

## 7. 其他組件（Other）

| 組件名稱           | Ant Design 對標  | 底層技術選型                    | 狀態 | 優先級 | 核心特性與動效                                        |
| :----------------- | :--------------- | :------------------------------ | :--: | :----: | :---------------------------------------------------- |
| **Affix**          | `Affix`          | 原生 CSS `sticky`               |  ⬜  |   P2   | 固釘組件、滾動時自動固定於頂部或底部                  |
| **App**            | `App`            | Context Provider 注入器         |  ⬜  |   P0   | 提供全域 Toast/Modal/Notification 的呼叫掛勾（Hooks） |
| **ConfigProvider** | `ConfigProvider` | 頂部 Theme / Direction Provider |  ⬜  |   P0   | 控制全域 Token、語言、方向（LTR/RTL）                 |
