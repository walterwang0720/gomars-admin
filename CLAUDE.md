# GOMARS 旅遊後台

## 專案目錄
```
/Users/walter/Downloads/Claude.platform/
```

## 主要檔案

| 檔案 | 說明 | 狀態 |
|------|------|------|
| `gomars_inquiry.html` | 供應商詢價單 | ✅ v1 結案 |
| `gomars_quote.html` | 成本報價單 | 🔧 開發中 |
| `gomars_admin.html` | 後台管理系統 | 🔧 開發中 |
| `contract_generator.html` | 合約產生器 | ✅ 完成 |
| `gomars_gifts.html` | 禮品報價模組 | ⏳ 待開發 |
| `gomars_base.css` | 共用基礎樣式 | — |

## 啟動方式
```bash
perl /tmp/gomars_server.pl
cp gomars_quote.html /tmp/index.html   # 換成要預覽的頁面
```
或直接用：`/preview [filename]`

## 技術規範

- **語言**：純 HTML + vanilla JS，單檔，無 build step
- **存檔**：純雲端（Supabase `gomars_cases`）；`.gomars` 僅備份匯出
- **詳細規格**：見 `.claude/rules/` 各檔案

## Roadmap（優先順序）

| Phase | 項目 | 優先度 |
|-------|------|--------|
| **A** | 報價單完成（A1 不使用zone → A2 預覽欄 → A3 列印 → A4 Word → A5 Supabase） | 高 |
| **B** | Admin：B1 Auth → B2 案件管理 → B3 儀表板 | 高 |
| **C** | CRM Supabase 串接（customers/follow_ups/orders） | 中 |
| **D** | 客報頁面 `gomars_client.html` | 中 |
| **E** | 禮品模組 `gomars_gifts.html` | 低 |
| **F** | 系統層：Edge Function / FX 自動更新 / LINE Notify / RLS | 低 |

## 快速指令

| 指令 | 用途 |
|------|------|
| `/preview [file]` | 複製頁面到 /tmp 並確認 server |
| `/deploy` | commit + push + vercel --prod |
| `/new-session` | 開場 context 模板 |
