# GOMARS 品牌規範（Design Tokens & Component Spec）

**適用範圍：** 所有 GOMARS 系統頁面（詢價單、航班 DB 管理、供應商比價…）
**來源：** `gomars_inquiry.html` `:root` 定義，v1 結案版

---

## 一、色彩 Token

### 品牌主色

| Token | Light | 說明 |
|---|---|---|
| `--orbit` | `#EA5404` | **主色調**：按鈕、Logo、section 序號角標 |
| `--mars` | `#C43A10` | **強調/Hover**：primary 按鈕 hover 狀態 |
| `--dust` | `#B85C00` | 輔助暗橘 |
| `--space` | `#0D0A08` | 近黑 |
| `--star` | `#F7F3EF` | 米白 |

### 功能色系（含 Dark Mode）

| 色系 | Token | Light | Dark |
|---|---|---|---|
| **綠（包含/確認）** | `--gr` | `#1D7A4E` | （同） |
| | `--grb`（背景） | `#E8F5EE` | `#1A2E22` |
| | `--grd`（強調文字） | `#145C39` | `#7ECDA0` |
| **藍（資訊/Focus）** | `--bl` | `#185FA5` | （同） |
| | `--blb`（背景） | `#EBF3FC` | `#1A2535` |
| | `--bld`（強調文字） | `#0C447C` | `#7BBCF5` |
| **橘棕（回程/旅館）** | `--br` | `#EA5404` | （同） |
| | `--brl`（背景） | `#FFF3E0` | `#2A1E0A` |
| | `--brm`（邊框） | `#F5C97A` | `#7A5020` |
| **灰階輔助** | `--g100` | `#F4F4F4` | `#2A2A2A` |
| | `--g400` | `#AAAAAA` | `#555` |
| | `--g600` | `#666` | `#888` |

### 背景

| Token | Light | Dark | 用途 |
|---|---|---|---|
| `--bg` | `#F4F1ED` | `#1A1714` | 頁面底色（溫暖米色） |
| `--bg-card` | `#FFFFFF` | `#241F1B` | Card / TopBar / 預覽欄 |
| `--bg-surface` | `#F7F5F2` | `#2C2621` | 輸入框、次級區塊 |

### 文字

| Token | Light | Dark | 用途 |
|---|---|---|---|
| `--tx` | `#1A1714` | `#F0EBE5` | 主文字 |
| `--tx2` | `#5A524A` | `#A89880` | 次要文字 |
| `--tx3` | `#9C9189` | `#6A5F55` | 標籤、說明、placeholder |

### 邊框

| Token | Light | Dark |
|---|---|---|
| `--border` | `#DDD8D2` | `#3A3028` |
| `--border-strong` | `#C5BDB5` | `#4A4038` |

---

## 二、字型

```css
--font: -apple-system, BlinkMacSystemFont, "PingFang TC", "Microsoft JhengHei",
        "SF Pro Text", "Segoe UI", sans-serif;
--font-mono: "SF Mono", "Fira Code", "Consolas", monospace;
```

- **基礎字級：** `13px`，`line-height: 1.5`
- **標籤（.lbl）：** `10px`，`font-weight: 600`，全大寫，`letter-spacing: .07em`
- **Logo：** `15px`，`font-weight: 800`，`letter-spacing: .08em`，色用 `--orbit`

---

## 三、間距 & 形狀

| Token | 值 | 用途 |
|---|---|---|
| `--radius` | `10px` | Card 圓角 |
| `--shadow` | `0 2px 12px rgba(0,0,0,.08)` | Card 陰影 |
| Card padding | `14px 16px` | `.card` 內距 |
| Card margin-bottom | `12px` | `.card` 間距 |
| TopBar height | `46px` | sticky 頂列高度 |

---

## 四、元件規格

### Card（`.card`）
```css
background: var(--bg-card);
border: .5px solid var(--border);
border-radius: var(--radius);  /* 10px */
padding: 14px 16px;
margin-bottom: 12px;
box-shadow: var(--shadow);
```
Section 序號角標（`.sec-num`）：`22×22px`，`background: var(--orbit)`，`border-radius: 6px`，白色文字 `11px/800`

---

### 按鈕（`.btn`）

| 類型 | 外觀 |
|---|---|
| 預設 | `bg: --bg-surface`，邊框 `--border`，文字 `--tx` |
| `.primary` | `bg: --orbit`，白字；hover → `bg: --mars` |
| `.ghost` | `background: transparent` |
| `.danger` | 透明底，邊框 + 文字 `#E55` |
| `.sm` | `padding: 4px 9px`，`11px` 字 |

TopBar 按鈕（`.tb-btn`）：`padding: 5px 11px`，`border-radius: 6px`，同上邏輯

新增按鈕（`.add-btn`）：虛線邊框，hover → 邊框/文字換 `--bl`，背景 `--blb`

---

### 輸入框（`.inp`）
```css
background: var(--bg-surface);
border: .5px solid var(--border);
border-radius: 7px;
padding: 7px 10px;
font-size: 13px;
```
- `:focus` → `border-color: var(--bl)`
- `[readonly]` → 文字色 `var(--br)`，`font-weight: 600`
- `textarea.inp` → `resize: vertical`，`min-height: 72px`

---

### Segment Control（`.seg` / `.seg-btn`）
- 容器：`bg: --bg-surface`，`border-radius: 7px`，`padding: 2px`
- 選中（`.on`）：`bg: --bg-card`，陰影 `0 1px 4px rgba(0,0,0,.1)`，`font-weight: 600`

---

### Chip（`.elem-chip`）
- 預設：`bg: --bg-surface`，`border-radius: 20px`，`12px`
- 選中（`:has(input:checked)`）：`bg: --blb`，`border-color: --bld`，`color: --bld`

---

### Info Box（`.info-box`）
| 變體 | 背景 | 邊框 | 文字 |
|---|---|---|---|
| 預設 | `--bg-surface` | `--border` | `--tx2` |
| `.green` | `--grb` | `#B2DAC8` | `--grd` |
| `.blue` | `--blb` | `#B5D4F4` | `--bld` |
| `.red` | `#FDE8E8` | `#FABABA` | `#A00` |

Dark `.red`：`bg: #2A1010`，`border: #6A2020`，`color: #F88`

---

### 航班方向標籤（`.flight-dir-label`）
- 去程（`.dir-out`）：`bg: --blb`，`color: --bld`
- 回程（`.dir-ret`）：`bg: #FAEEDA`，`color: #633806`（Dark：`bg: #2A1E0A`，`color: #F5C97A`）

### 天數徽章（`.day-num-badge`）
- `color: --orbit`，`bg: --brl`，`border: --brm`，`border-radius: 5px`

### 餐食按鈕（`.mb`）狀態色
| 狀態 | 邊框/文字 | 背景 |
|---|---|---|
| `.on-inc`（含餐） | `--gr` | `--grb` |
| `.on-exc`（自理） | `--g400` / `--g600` | `--g100` |
| `.on-arr`（協助安排） | `--br` | `--brl` |
| `.on-res`（指定餐廳） | `--bl` | `--blb` |
| `.on-flt`（飛機餐） | `#7B5EA7` | `#F3EEF9` |

---

## 五、版型

- **主版型：** 左側表單欄（`flex:1`）+ 右側預覽欄（`width: 300px`）
- **預覽欄隱藏：** `.hidden` → `width: 0`
- **RWD 斷點：** 900px 收起預覽欄；600px 單欄 layout
- **Grid 輔助：** `.g2`（2欄）、`.g4`（4欄），`.full` = `grid-column: 1/-1`

---

## 六、Dark Mode

切換方式：`document.documentElement.setAttribute('data-theme', 'dark')`
所有 token 在 `[data-theme="dark"]` 中覆寫，**不需要額外 class**。

---

## 七、開發原則

1. **新頁面一律沿用同一套 `:root` token**，不得硬寫色碼。
2. 主要 CTA 按鈕統一用 `--orbit` → hover `--mars`。
3. 成功/確認狀態用綠色系（`--gr`），資訊/連結用藍色系（`--bl`），警告/回程用橘棕系（`--br`）。
4. 邊框統一用 `.5px solid var(--border)`，重點邊框用 `--border-strong`。
5. 字型不另設定，沿用 `var(--font)`。
