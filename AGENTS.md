# 專案名稱：GeoAI 空間資訊大模型應用庫 (GeoAI & Spatial LLM Wiki)

> 本文件結合 **Andrej Karpathy LLM Wiki** 知識累積模式與 **GeoAI 靜態網頁展示規範**，作為 AI Agent 維護本知識庫的最高指導原則（Schema）。所有溝通、筆記與網頁內容一律使用**繁體中文（台灣）**。

---

## 1. 專案目的
本專案是一個記錄「空間資訊、測量工程與大型語言模型 (LLM) 結合應用」的複合式個人知識庫與靜態知識庫網站。旨在系統化地整理無人機影像辨識、Google Earth Engine 程式碼生成、以及空間數據 RAG 系統的原始文獻、編譯筆記與網頁文章，方便未來持續累積、交叉引用並快速對外展示。

---

## 2. 網頁與內容風格 (Design System)
- **UI 框架**：使用純 HTML + Tailwind CSS (透過 CDN 引入)。
- **色彩配置 (工程科技風)**：
  - 側邊欄與背景：深邃的科技藍黑 (`bg-slate-900`, `text-slate-300`)。
  - 內容主區塊：純白背景 (`bg-white`)，文字使用深灰 (`text-slate-800`)。
  - 強調色：標題或重要按鈕使用亮藍色 (`text-blue-600`, `bg-blue-600`)。
- **排版結構**：
  - 左側：固定寬度的導覽選單 (Sidebar)，條列所有技術筆記。
  - 右側：主要內容區 (Main Content)。
  - 響應式：手機版需將側邊欄改為上方漢堡選單或折疊。

---

## 3. 專案結構與檔案命名
```text
LLM Wiki/
├── index.html            # 網站首頁（知識庫簡介、三大應用軸線與近期更新）
├── AGENTS.md             # AI 開發與知識庫維護規則指南 (本文件)
├── README.md             # 專案操作與 Obsidian / 瀏覽器預覽說明
├── assets/               # 網頁靜態資源 (圖片、圖示、範例圖表等，可選)
├── raw/                  # [Raw層] 原始資料來源（絕對唯讀，禁止修改或刪除）
│   ├── papers/           #   論文、技術報告 PDF 或 Markdown
│   ├── articles/         #   使用者貼上的文章、網頁剪藏
│   ├── notes/            #   零散研究筆記、實驗數據、Prompt 紀錄
│   └── assets/           #   原始文章附帶的本地圖片
└── wiki/                 # [Wiki層] 編譯後的知識庫（Markdown 知識節點 + HTML 展示頁）
    ├── index.md          #   內容導向 Markdown 總目錄
    ├── log.md            #   時間導向操作日誌（Append-only，前綴 ## [YYYY-MM-DD] <op> | <title>）
    ├── overview.md       #   GeoAI 全域研究總覽與演化脈絡
    ├── sources/          #   每份 raw/ 原文的結構化摘要 (.md)
    ├── concepts/         #   技術概念與方法論筆記 (.md)
    ├── entities/         #   模型、平台、工具套件實體頁 (.md)
    ├── comparisons/      #   技術方案或模型橫向比較 (.md)
    ├── synthesis/        #   跨來源深度綜述與問答沉澱 (.md)
    ├── uav-vision.html   #   網頁筆記：多模態 LLM 無人機影像特徵辨識
    ├── gee-copilot.html  #   網頁筆記：GEE 遙測程式碼自動生成
    ├── yolo-deepsort.html #  網頁筆記：YOLOv8 + DeepSORT 無人機車流追蹤與 TWD97 映射
    └── lidar-rag.html    #   網頁筆記：光達點雲操作手冊與測量法規 RAG 系統
```

---

## 4. 雙軌知識庫工作流程 (Karpathy Wiki + GeoAI HTML)

### A. 吸收新文章（Ingest）
當使用者貼上新文章或將資料放入 `raw/` 時，AI 必須依序完成以下雙軌作業：
1. **保存原文至 `raw/`**：若使用者直接貼上文章內容，先將原文完整保存至 `raw/articles/`（或 `raw/papers/` / `raw/notes/`），檔名採 `YYYY-MM-DD-<slug>.md`；`raw/` 內容建立後即視為唯讀事實來源（Source of Truth）。
2. **編譯 Markdown 知識節點**：
   - 在 `wiki/sources/` 建立來源摘要頁，並更新或新增相關的 `wiki/concepts/`、`wiki/entities/`、`wiki/comparisons/` 頁面，附上 YAML Frontmatter 與 `[[wikilinks]]` 雙向連結。
   - 若新資料與舊有數據或觀點衝突，使用 `> [!warning] 觀點衝突 / 資料更新` 明確標註，不可靜默刪除舊紀錄。
   - 同步更新 `wiki/index.md` 與 `wiki/overview.md`，並在 `wiki/log.md` 追加一筆 `ingest` 紀錄。
3. **產出或更新 HTML 展示頁**：依下方「AI 新增內容與修改規則」生成或更新對應的 `wiki/*.html` 與全站側邊欄。

### B. 查詢與問答沉澱（Query）
- 優先讀取 `wiki/index.md` 與 `wiki/overview.md` 定位相關 Markdown 筆記，回答時附上引用來源。
- 有價值的綜合比較或探索結論，可經確認後沉澱為 `wiki/synthesis/` 或新的 `wiki/*.html` 頁面，並寫入 `wiki/log.md`（標記 `query`）。

### C. 知識庫健檢（Lint）
- 定期檢查：頁面間的數據矛盾或過時宣稱、孤島頁面（無連入連結）、`wiki/index.md` 與實際檔案同步狀態，以及所有 `.html` 側邊欄與相對路徑是否皆可正常連通，完成後於 `wiki/log.md` 追加 `lint` 紀錄。

---

## 5. AI 新增內容與修改規則 (AI Instructions)
當你 (AI) 被要求「新增或修改一篇技術筆記（HTML 網頁）」時，請嚴格遵守以下流程：
1. **繼承版型**：必須讀取並沿用 `index.html` 的 HTML 結構，保留完整的 `<nav>` (側邊欄) 與手機版漢堡選單腳本，僅替換 `<main>` 內容。
2. **內容排版規範**：
   - 大標題使用 `<h1 class="text-3xl font-extrabold text-slate-800 mb-6 border-b pb-2">`。
   - 程式碼區塊必須使用 `<pre><code class="bg-slate-800 text-gray-100 p-4 rounded-lg block overflow-x-auto my-4">` 包覆。
   - 技術名詞 (如 GNSS, YOLO, RAG, GEE, GSD, VLM) 需使用粗體 `<span class="font-semibold text-blue-600">` 強調。
3. **自動更新導覽列 (重要！)**：每新增一個 `/wiki/xxx.html` 檔案，必須同步修改所有現有 `.html` 檔案的側邊欄，將新頁面的連結加入，並確保相對路徑正確（例如在 `index.html` 中使用 `wiki/xxx.html`；在 `wiki/*.html` 中連回首頁使用 `../index.html`、互連筆記使用 `xxx.html` 或 `../wiki/xxx.html`）。
4. **同步日誌與索引**：完成 HTML 新增或修改後，同步更新 `wiki/index.md` 與追加 `wiki/log.md`。
