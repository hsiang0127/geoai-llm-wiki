# 操作日誌（Wiki Log）

> 本檔案為時間導向的只追加（Append-only）紀錄。每筆紀錄標題固定以 `## [YYYY-MM-DD] <operation> | <簡短標題>` 開頭，便於回溯與檢索。

## [2026-11-16] init | 初始化 LLM 研究知識庫
- **摘要**：依據 Karpathy LLM Wiki 架構建立繁體中文 `AGENTS.md`、`raw/`、`wiki/`、`templates/` 目錄結構與核心索引檔案。
- **影響頁面**：[[index]]、[[overview]]、[[log]]

## [2026-11-16] schema | 確立 GeoAI 雙軌規範並建立首篇靜態 HTML 筆記
- **摘要**：將 `AGENTS.md` 改版為「GeoAI 空間資訊大模型應用庫」雙軌規範（整合 `raw/`、`index.md`、`log.md` 與 Tailwind HTML 靜態網站規則），並生成 `index.html`、`wiki/uav-vision.html`（含 Python / Gradio 範例）及對應概念筆記。
- **影響頁面**：`AGENTS.md`、`index.html`、`wiki/uav-vision.html`、[[uav-multimodal-thickness-estimation]]、[[index]]、[[overview]]

## [2026-11-16] ingest | GEE Copilot：利用大語言模型自動生成遙測分析腳本
- **摘要**：將使用者提供之 GEE Copilot 草稿保存至 `raw/articles/2026-11-16-gee-copilot-draft.md`，建立來源摘要、概念頁與 `wiki/gee-copilot.html`，並同步更新 `index.html`、`wiki/uav-vision.html` 側邊欄與 `wiki/index.md`、`wiki/overview.md`。
- **影響頁面**：`raw/articles/2026-11-16-gee-copilot-draft.md`、[[2026-11-16-gee-copilot-draft]]、[[gee-copilot-prompt-generation]]、`wiki/gee-copilot.html`、`wiki/uav-vision.html`、`index.html`、[[index]]、[[overview]]

## [2026-11-16] ingest | GeoAI 實戰：基於 YOLOv8 與 DeepSORT 的無人機車流追蹤與座標映射
- **摘要**：將使用者提供之 UAV 車流追蹤文章保存至 `raw/articles/2026-11-16-yolo-deepsort-uav-traffic.md`，建立來源摘要、概念頁與 `wiki/yolo-deepsort.html`，並同步更新 `index.html`、`wiki/uav-vision.html`、`wiki/gee-copilot.html` 側邊欄與 `AGENTS.md`、`wiki/index.md`、`wiki/overview.md`。
- **影響頁面**：`raw/articles/2026-11-16-yolo-deepsort-uav-traffic.md`、[[2026-11-16-yolo-deepsort-uav-traffic]]、[[uav-traffic-tracking-twd97]]、`wiki/yolo-deepsort.html`、`wiki/uav-vision.html`、`wiki/gee-copilot.html`、`index.html`、[[index]]、[[overview]]

## [2026-11-16] query | 補齊光達操作手冊 RAG 系統筆記並完成四軸線網站建置
- **摘要**：建立 `wiki/lidar-rag.html` 與對應概念筆記 [[lidar-manual-rag-architecture]]，並同步更新 `index.html`、`wiki/uav-vision.html`、`wiki/gee-copilot.html`、`wiki/yolo-deepsort.html` 側邊欄及 `AGENTS.md`、`wiki/index.md`、`wiki/overview.md`，全站四大應用規劃皆已上線互通。
- **影響頁面**：`wiki/lidar-rag.html`、[[lidar-manual-rag-architecture]]、`index.html`、`wiki/uav-vision.html`、`wiki/gee-copilot.html`、`wiki/yolo-deepsort.html`、`AGENTS.md`、[[index]]、[[overview]]
