# GOMARS 旅遊後台開發說明

## 專案目錄
```
/Users/walter/Downloads/Claude.platform/
```

## 主要檔案
| 檔案 | 說明 | 狀態 |
|------|------|------|
| `gomars_inquiry.html` | 供應商詢價單（~2340 行） | 純雲端化完成 ✅ |
| `gomars_quote.html` | 成本報價單（~2200 行） | 開發中 |
| `gomars_admin.html` | 後台管理系統（~2500 行） | 開發中 |
| `GOMARS_開發日誌.md` | 完整功能清單、技術參考、未來規格 | 必讀 |
| `GOMARS_品牌規範.md` | 設計 token、元件規格 | 設計參考 |

## 啟動方式
```bash
perl /tmp/gomars_server.pl
cp gomars_quote.html /tmp/index.html   # 或其他頁面
```

## 關鍵技術
- **語言**：純 HTML + vanilla JS，單檔，無 build step
- **存檔格式**：純雲端（Supabase `gomars_cases`）；`.gomars` 僅作備份匯出用途
- **LocalStorage key**：
  - `gomars_inquiry_draft`（詢價單草稿）
  - `gomars_flight_db`（航班資料庫本地快取）
- **Supabase**：用於 auth + 案件管理 + **航班資料庫雲端同步**
  - `gomars_cases` 表：案件主表，含 inquiry_data / quote_data / status / soft-delete
  - `flight_db` 表：`flight_no / airline / from / to / dep / arr / updated_at`
  - **inquiry 存檔**：`saveToCloud()` → SELECT 最新版本 → version+1 → upsert `gomars_cases` + 同步變動航班；版本寫入 `inquiry_data._version`
  - **admin 案件列表**：`loadCases()` → SELECT from Supabase（排除 deleted）
  - **soft delete**：`status='deleted'` + `deleted_at`；30 天後 Edge Function 清理
  - 策略：LocalStorage 僅快取航班資料庫（UI 不阻塞），案件資料純 Supabase
- **已移除**：夜間模式（`[data-theme="dark"]` CSS 全面清除）；本機下載/載入功能
- **CSS token**：`--mars:#C43A10` `--orbit:#EA5404` `--gr:#1D7A4E` `--bl:#185FA5`

## gomars_quote.html 目前狀態（2026-04-06）
- ✅ 逐項計算模式：`calcAll()` 完整運作，8 大 section + 其他費用 + summary + 定價
- ✅ 淨報模式完整重設計（見開發日誌四-C）：
  - 拖拉分類區（SortableJS）：廠商 NET 包含 / 我方另加 / 待做：不使用 zone
  - 供應商 NET 報價（每人）＋ 包含項目自動標籤
  - 我方另加費用表格（同 other-costs 新增列邏輯）
  - 成本合計條（廠商 + 我方 = 合計）
  - 刷卡手續費欄位（%，加入售價計算）
  - 毛利 / 利潤率可手動填，三向連動（改毛利或改利潤率 → 回推成人售價）
- ⏳ 待完成：不使用 zone、右側即時預覽欄、列印版型、Word 匯出、Supabase 儲存

## gomars_inquiry.html UI 架構（2026-04-06 精簡後）
- Topbar：標題 + 儲存狀態（dot / 文字 / ver-chip）+ 清除重填 + 預覽欄切換
- Action Bar：案號 badge + 儲存案件 + 列印/匯出 + 轉報價（iframe 才顯示）
- 草稿還原通知改為 toast（不再有 banner）
- 版本 counter 從 Supabase `inquiry_data._version` 讀取，確保多 tab 不衝突

## 下次可接手的開發項目（優先順序）
1. **admin.html Supabase Auth**（中）— 登入後 `owner` 自動帶入 `sb.auth.getUser().email`
2. **淨報模式 — 不使用 zone**（小）— gomars_quote.html，第三個 drop zone，chip 拖入後灰化
3. **右側即時預覽欄**（中）— gomars_quote.html，顯示各 section 金額 + 每人成本 + 售價
4. **列印版型 `@media print`**（中）— 成本版 / 客報版（隱藏成本）
5. **客報頁面 `gomars_client.html`**（大）— 行程排版 HTML，含飯店/景點資料庫圖文

詳細規格見 `GOMARS_開發日誌.md`。
