# GOMARS 供應商詢價單

## 專案檔案
- 主檔：`gomars_inquiry.html`（約 2247 行，pure HTML + vanilla JS 單檔）
- 開發日誌：`GOMARS_開發日誌.md`（完整功能清單、技術參考、未來規格）

## 啟動方式
```bash
perl /tmp/gomars_server.pl        # 啟動預覽 server
cp gomars_inquiry.html /tmp/index.html  # 同步到 server
```

## 目前版本狀態
v1 結案。所有核心功能完整，可正常使用。

## 關鍵技術
- 存檔格式：`.gomars`（JSON），含完整 `_save` 物件可全欄位還原
- LocalStorage：`gomars_inquiry_draft`（草稿）、`gomars_flight_db`（航班 DB）
- Word 匯出：HTML Blob → `.doc`，`@page Section1` 設 10mm 四邊窄邊距
- CSS token：`--mars:#C43A10` `--orbit:#EA5404` `--gr:#1D7A4E` `--bl:#185FA5`

## 下次可接手的開發項目
1. **航班資料庫管理 UI**（高優先）— 查看 / 編輯 / 刪除 `gomars_flight_db`
2. **詢價單範本系統** — 常見行程一鍵帶入
3. **供應商比價模式** — 同一張詢價單對應多家供應商，批次匯出
4. **匯率即時更新** — fetch 免費 API 取代寫死的 `RATES`
5. **梯次團模式** — 企業員旅分批出發，梯次總覽表 + 各梯次航班

詳細規格見 `GOMARS_開發日誌.md` 第三章。
