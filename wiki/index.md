# 知識庫總目錄（Wiki Index）

> 本檔案為內容導向導航索引，由 Agent 在每次 `ingest`、`query`（歸檔）、`lint` 或新增 HTML 筆記後同步更新。

## 總覽與研究綜述（Overview & Synthesis）
- [[overview|GeoAI 空間資訊大模型應用庫總覽]] — 涵蓋 UAV 多模態影像、GEE Copilot 與光達 RAG 三大核心軸線。（更新：2026-11-16）

## 網頁展示頁面（HTML Pages）
- `index.html` — GeoAI 空間資訊大模型應用庫靜態網站首頁與導覽總覽。（更新：2026-11-16）
- `wiki/uav-vision.html` — 範例筆記：利用多模態大模型推算無人機拍攝食材厚度與空間尺度（含 Python / Gradio 程式碼）。（更新：2026-11-16）
- `wiki/gee-copilot.html` — 技術筆記：GEE Copilot 利用大語言模型自動生成遙測分析腳本（含新竹市 NDVI 範例）。（更新：2026-11-16）
- `wiki/yolo-deepsort.html` — 技術筆記：基於 YOLOv8 與 DeepSORT 的無人機車流追蹤與 TWD97 座標映射。（更新：2026-11-16）
- `wiki/lidar-rag.html` — 技術筆記：光達（LiDAR）操作手冊與測量法規 RAG 檢索系統（含 Python Hybrid Search 原型）。（更新：2026-11-16）

## 核心概念（Concepts）
- [[uav-multimodal-thickness-estimation|無人機多模態影像厚度與空間尺度推算]] — 結合 GSD、校正標靶與 VLM Prompt 約束進行尺度與厚度推理（對應 `wiki/uav-vision.html`）。（更新：2026-11-16）
- [[gee-copilot-prompt-generation|GEE Copilot 與遙測程式碼生成]] — 透過結構化 Prompt 將自然語言轉為 GEE Python 遙測腳本，並探討結合 RAG 降低 API 幻覺（對應 `wiki/gee-copilot.html`）。（更新：2026-11-16）
- [[uav-traffic-tracking-twd97|無人機車流追蹤與 TWD97 空間座標映射]] — 整合 YOLOv8n-visdrone、DeepSORT 與共線方程式映射至 TWD97（對應 `wiki/yolo-deepsort.html`）。（更新：2026-11-16）
- [[lidar-manual-rag-architecture|光達操作手冊與測量法規 RAG 檢索架構]] — 結構化切片、Hybrid Search 與條文溯源 Prompt 設計（對應 `wiki/lidar-rag.html`）。（更新：2026-11-16）

## 模型、機構與專案實體（Entities）
*（尚未新增實體頁，待吸收更多工具或平台文件後建立）*

## 橫向比較與評測（Comparisons）
*（尚未新增比較頁，可透過 Ingest 或 Query 沉澱建立）*

## 原始來源摘要（Sources）
- [[2026-11-16-gee-copilot-draft|GEE Copilot：利用大語言模型自動生成遙測分析腳本（草稿摘要）]] — 記錄新竹市 Sentinel-2 NDVI 分析情境與未來結合 RAG 展望。（更新：2026-11-16）
- [[2026-11-16-yolo-deepsort-uav-traffic|GeoAI 實戰：基於 YOLOv8 與 DeepSORT 的無人機車流追蹤與座標映射（來源摘要）]] — 整理 UAV 邊緣偵測、DeepSORT 追蹤與 TWD97 共線方程式映射流程。（更新：2026-11-16）
