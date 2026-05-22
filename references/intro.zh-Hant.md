# GitHub技術週報

這個 skill 用於生成、維護和發布單檔版 GitHub 技術週報 HTML。它適合處理 GitHub 一週熱榜、一個月熱榜和飆升榜這類排行榜頁面，並要求頁面可以直接打開，不依賴本地建置流程。

## 能做什麼

- 生成或更新克制的技術編輯類排行榜頁面。
- 維護簡體中文、繁體中文和英語三種語言切換。
- 本地化頁面標題、分區說明、榜單摘要、彈窗項目介紹、作用說明和使用建議。
- 保留彈窗的關閉按鈕、遮罩關閉、Esc 關閉和鍵盤可訪問性。
- 驗證 HTML 檔案存在、內聯腳本可解析、語言按鈕存在、榜單排序連續、項目介紹走本地化路徑。
- 在使用者要求時把報告或 skill 發布到 GitHub。

## 使用方式

讓支援 skill 的 agent 載入 `github-technical-weekly-report`，並提供目標 HTML 檔案或說明要新生成一份週報。更新後應執行本地驗證腳本；如果要上傳 GitHub，應確認目標倉庫、分支和檔案路徑，再透過 GitHub connector、Git CLI 或網頁上傳。

## 通用性

通用核心是 `SKILL.md` 和 `references/`。`agents/openai.yaml` 只是 OpenAI/Codex 的可選 UI metadata，其他 agent 平台可以忽略。
