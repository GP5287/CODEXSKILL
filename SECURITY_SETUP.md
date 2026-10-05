# CODEXSKILL 安全設定規劃

更新日期：2026-10-06（Asia/Taipei）
目標儲存庫：https://github.com/GP5287/CODEXSKILL

## 使用原則

僅使用免費方案，不查詢付費資格、不升級。此儲存庫為公開儲存庫。
已於 GitHub 儲存庫安全設定頁實際確認與設定；下列狀態記錄 2026-10-06 的結果。

## 三項安全功能

| 功能 | 用途 | 目前狀態 |
|---|---|---|
| Secret Scanning / Push Protection | 偵測已提交的受支援 secrets，並在推送時阻擋可識別的 secrets | 已確認 Secret Protection 與 Push protection 均啟用（原本已開啟） |
| Dependabot | 已知依賴漏洞警示及安全更新 PR；按套件管理器設定版本更新 | 已啟用 Dependency graph、Dependabot alerts、Dependabot security updates；尚無依賴清單，version updates 待加入依賴後設定 |
| CodeQL / Code Scanning | 分析支援語言的程式碼漏洞 | 已啟用 Default setup（預設高精確度查詢）；尚無支援語言，GitHub 會於 main 出現支援語言後自動執行首次掃描 |

## 設定與後續步驟

1. 開啟儲存庫 Settings 的安全設定頁。
2. 確認 Secret Scanning 已啟用，啟用 Push Protection。
3. 啟用 Dependency graph、Dependabot alerts 與 Dependabot security updates。
4. 在 Code scanning / CodeQL analysis 選擇 Default setup，採用預設查詢組。
5. 加入實際程式碼及依賴清單後，確認首次掃描結果，並依目錄和套件管理器設定每週 Dependabot version updates。
6. 更新 PR 經測試及審查後再合併，不自動合併所有套件更新。

CodeQL 支援 Python、JavaScript／TypeScript、C#、C/C++ 等語言；GDScript 不在官方支援清單中。若儲存庫只有 Markdown 技能檔案，CodeQL 不會因此完成程式碼分析。

## 外掛技能檢查

NVIDIA SkillSpector 可補充技能檔案、腳本及 MCP 相關模式的檢查。
使用靜態模式 `--no-llm`，不執行受檢技能的腳本。
掃描器警示需要搭配來源與覆蓋範圍判讀；不代表可取代金鑰、依賴或程式碼檢查。

## 官方文件

- [Secret scanning](https://docs.github.com/en/code-security/how-tos/secure-your-secrets/detect-secret-leaks/enable-secret-scanning)
- [Push protection](https://docs.github.com/en/code-security/concepts/secret-security/about-alerts)
- [Dependabot](https://docs.github.com/en/code-security/concepts/supply-chain-security/dependabot-version-updates)
- [CodeQL default setup](https://docs.github.com/en/code-security/how-tos/find-and-fix-code-vulnerabilities/configure-code-scanning/configure-code-scanning)
- [NVIDIA SkillSpector](https://github.com/NVIDIA/SkillSpector)
