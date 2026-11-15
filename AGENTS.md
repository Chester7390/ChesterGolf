# AGENTS.md - 高爾夫海外網購與運動心理知識庫開發規範

## 1. 專案目的 (Project Purpose)
本專案是一個模組化的靜態知識庫網站（Golf Knowledge Hub），旨在提供高爾夫球友實用的「海外球具代購指南（含日本 Mercari / ZenMarket 試算與海關關稅規則）」、「高爾夫球場規則解析」以及「擊球心理素質建立」文章。
所有頁面皆採用純 HTML5 與 CSS3 開發，確保無需複雜編譯即可部署於 GitHub Pages，並能讓 AI 依據本規範快速新增標準化頁面。

## 2. 整體視覺風格 (Design System & Aesthetics)
- **設計主題**：果嶺清新運動風（Clean Fairway Minimalist），強調高可讀性與清晰的重點提示。
- **色彩規範 (CSS Variables)**：
  - 主色調 (Primary Green): `#1b4332`（深果嶺綠，用於導覽列、主標題）
  - 強調色 (Accent Green): `#2d6a4f`（草地綠，用於按鈕、標籤、重點左邊框）
  - 淺色背景 (Background): `#f8faf9`（極淺灰綠，減少閱讀疲勞）
  - 卡片背景 (Card Surface): `#ffffff`（純白，搭配 `1px solid #e2e8f0` 邊框與微陰影）
  - 警示/重點提示框 (Callout Box): 背景 `#fefae0`、左邊框 `4px solid #d4a373`（沙坑金，用於稅率公式或罰桿提醒）
- **字體規範**：優先使用系統無襯線字體（`'Noto Sans TC', -apple-system, BlinkMacSystemFont, sans-serif`），內文行高固定為 `1.75` 以利長文閱讀。

## 3. 檔案命名與目錄結構 (Directory & Naming Conventions)
- 根目錄僅放置 `AGENTS.md`、`index.html` 與 `style.css`。
- 所有獨立知識文章一律放置於 `/articles/` 資料夾內。
- **檔名規則**：必須使用全小寫英文與連字號（kebab-case），嚴禁使用中文或空格。
  - 正確範例：`articles/import-tax-guide.html`、`articles/ob-penalty-rules.html`
  - 錯誤範例：`articles/關稅教學.html`、`articles/OB rules.html`

## 4. 頁面 HTML 結構規範 (Page Structure)
### A. 文章內頁 (`/articles/*.html`) 必須包含以下區塊：
1. `<head>`：必須引入上層的樣式表 `<link rel="stylesheet" href="../style.css">`，並設定正確的 `<title>文章標題 | 高爾夫知識庫</title>`。
2. `<header class="navbar">`：包含網站名稱與「← 返回知識庫首頁 (`../index.html`)」連結。
3. `<main class="article-container">`：
   - `<div class="article-meta">`：包含分類標籤（如 `[海外網購]`、`[球場規則]`、`[運動心理]`）與更新日期。
   - `<h1>`：文章主標題。
   - `<div class="callout-box">`：文章開頭的「核心懶人包 / 重點摘要」。
   - `<section>` 與 `<h2>`：分段落的詳細內容（若有計算公式或步驟，必須使用 `<ul>`、`<ol>` 或 `<table>` 呈現）。
4. `<footer>`：統一版權聲明。

### B. 首頁 (`index.html`) 卡片結構：
首頁使用 `.card-grid` 網格排版，每篇文章對應一個 `<a class="article-card" href="articles/檔名.html">` 卡片，內含分類標籤、標題與兩行以內的簡介。

## 5. AI 新增或修改內容的執行規則 (Rules for AI Agents)
當使用者要求「新增一篇關於 XXX 的文章或頁面」時，AI 必須嚴格執行以下工作流：
1. **確認分類與命名**：根據主題決定分類標籤（`海外網購`、`球場規則`、`運動心理` 或 `球具評測`），並生成符合 kebab-case 的英文檔名（如 `articles/driver-loft-guide.html`）。
2. **建立獨立頁面**：嚴格套用第 4 節定義的 HTML 結構與 `../style.css` 的既有 class 名稱，**嚴禁在 HTML 檔案中寫行內樣式 (inline CSS) 或自行新增 `<style>` 標籤**。
3. **同步更新首頁**：建立新文章後，**必須自動開啟 `index.html`**，在 `.card-grid` 區塊的最前方（最新文章優先）插入對應的 `<a class="article-card">` 連結卡片，確保首頁能直接點擊進入新頁面。
4. **保持既有樣式**：除非使用者明確要求修改全站設計，否則不得更動 `style.css` 的既有規則。
