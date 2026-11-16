# GeoAI 空間資訊大模型應用庫 (GeoAI & Spatial LLM Wiki)

本專案結合 **Karpathy LLM Wiki**（知識編譯與索引系統）與 **Tailwind CSS 靜態網站**，用於長期累積「空間資訊、測量工程與 LLM 結合應用」的研究資料、技術筆記與程式碼範例。

## 快速瀏覽網頁
- 直接用瀏覽器開啟根目錄的 `index.html`，即可看到左側工程科技風導覽列與首頁總覽，並可點擊進入 `wiki/uav-vision.html`（支援桌面固定側邊欄與手機版漢堡選單）。

## 雙軌目錄結構
- `AGENTS.md`：AI 開發與知識庫維護規則（包含 HTML Design System 與 Ingest/Query/Lint 流程）。
- `index.html`：靜態網站首頁。
- `assets/`：網頁靜態資源（圖片、範例圖表等）。
- `raw/`：**原始資料層（唯讀）**，所有貼給 Agent 的論文與文章都會完整保存於此（`papers/`、`articles/`、`notes/`、`assets/`）。
- `wiki/`：**知識編譯與網頁層**，包含 Markdown 索引與筆記（`index.md`、`log.md`、`overview.md`、`concepts/` 等）以及對應的靜態網頁（`uav-vision.html` 等）。

## 日常使用方式
1. **吸收新文章**：直接把文章內容貼給 Agent，或將 PDF / Markdown 放進 `raw/`，Agent 會先保存原文至 `raw/`，再編譯更新 Markdown 筆記、`wiki/index.md`、`wiki/log.md` 與對應的 `wiki/*.html` 頁面及全站側邊欄。
2. **搭配 Obsidian（選用）**：用 Obsidian 開啟本資料夾作為 Vault，可同時透過雙向連結與圖譜檢視所有 `.md` 筆記。
