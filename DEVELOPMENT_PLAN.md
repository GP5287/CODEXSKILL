# 開發與部署路線

更新日期：2026-10-06（Asia/Taipei）。僅使用免費方案，不查詢付費資格、不升級。
本文件為建議流程，尚未設定排程、部署服務或新增外掛。

## 目前階段

已安裝 GitHub、Context7、Supabase、Figma 與 SkillSpector。
CODEXSKILL 已啟用／確認 Secret Protection、Push protection、Dependency graph、Dependabot alerts、Dependabot security updates、CodeQL Default setup。
目前仍是環境與安全準備階段，尚無遊戲、交易應用、行情資料管線或產品部署。
先前 Figma / Supabase 靜態掃描有警示與部分涵蓋項目，不能視為所有外掛已通過完整稽核；後续使用相关功能前需處理對應警示。

## 現階段需要補齊的項目

| 優先 | 項目 | 原因與建議 |
|---|---|---|
| 立即 | 專案與執行環境 | CODEXSKILL 作為規則／技能管理庫；遊戲與交易研究分開管理。決定遊戲引擎、程式語言及交易市場後才安裝對應工具。 |
| 立即 | 重現與版本管理 | 專案專用虛擬環境、依賴鎖定、版本記錄；掃描器也固定版本並保存報告。 |
| 第一個功能時 | 測試與 CI | 按專案語言設定 GitHub Actions：必要測試、建置、CodeQL 與對應技能掃描。先確定檢查能成功，再將 main 的 PR／必要狀態檢查設為合併條件。 |
| 交易原型時 | 行情資料來源 | 確定台股／美股／期貨／加密貨幣及日線／分鐘線。先驗證免費資料的历史范围、頻率、調整方式、使用限制與缺漏，再決定 API。 |
| 交易原型時 | 本機分析資料 | 可評估 Python + DuckDB / Parquet 儲存及 SQL 篩選历史行情。交易紀錄、策略設定及網頁共用資料再考慮 Supabase。 |
| 接入資料庫前 | 權限與備份 | 規劃 RLS、遷移、環境金鑰、備份及還原測試。免費 Supabase 專案依官方建議定期匯出並保留站外備份；不要把真實交易資料或備份放進公開 GitHub。 |
| 上線前 | 部署與回退 | 先測試環境與模擬資料，確認功能、權限、日誌、備份與回退，再部署選定平台。 |

## 外掛建議

目前先沿用已安裝的四項整合，不再新增外掛。
已有 Context7 查文件、GitHub 管版本與檢查、Figma 設計介面、Supabase 管雲端資料。
錯誤監控與產品分析等到有可運作的網站／遊戲再評估；目錄有 PostHog，适合届时研究事件與錯誤追蹤，但本次不安裝，也尚未確認其掃描範圍或具體免費方案限制。
DuckDB、遊戲引擎、行情 API 與回測函式庫屬於開發工具／資料服務，應依實際需求選擇，不以裝 Codex 外掛取代。

## 後續建議流程

1. 確定第一個目標：遊戲原型，或交易紀錄／條件選股。補齊遊戲引擎、交易市場與資料頻率。
2. 建立對應專案，加入 AGENTS.md、忽略敏感檔案、固定依賴與基本說明。
3. 每次加入外掛或新功能：取得可掃描來源 → SkillSpector 靜態檢查 → 核對警示及涵蓋範圍 → 必要修正 → 最小功能實作 → 測試／適用的安全檢查。
4. 交易方向先完成「模擬成交 CSV → 交易紀錄 → 損益／手續費」。接著做單一資料來源與單一選股條件，最後加入回測；記錄成交時間、資料可得時間、費用、滑價與調整方式，避免未來資料影響歷史決策。
5. 遊戲方向先完成可操作的最小場景、核心玩法與存檔，再接介面、雲端功能及擴充內容。
6. 確認 CI 可運作後設定 main 的合併規則，依實際依賴建立 dependabot.yml。不要在只有 Markdown 的庫加入不適用的程式分析工作流程。
7. 測試環境驗證、備份／還原演練與回退準備完成後部署；上線後才補需要的錯誤監控與產品分析。

## 參考文件

- [DuckDB Python](https://duckdb.org/docs/stable/clients/python/overview)
- [Supabase 免費專案備份建議](https://supabase.com/docs/guides/platform/backups)
- [GitHub protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
- [NVIDIA SkillSpector](https://github.com/NVIDIA/SkillSpector)
