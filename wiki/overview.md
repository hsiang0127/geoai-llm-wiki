---
title: "GeoAI 空間資訊大模型應用庫總覽（GeoAI & Spatial LLM Overview）"
type: synthesis
tags:
  - geoai
  - spatial-llm
  - overview
created: 2026-11-16
updated: 2026-11-16
status: seed
sources: []
---

# GeoAI 空間資訊大模型應用庫總覽

> 本頁彙整「空間資訊、測量工程與大型語言模型（LLM）結合應用」的核心研究方向與網頁筆記規劃。

## 核心研究與應用軸線
1. **無人機多模態影像辨識（`wiki/uav-vision.html`）**：結合 Gemini Pro Vision 等視覺語言模型（VLM）與航拍空間幾何（GSD、校正標靶、斜拍陰影），進行物件偵測、厚度估算與空間尺度推論。
2. **Google Earth Engine 遙測程式自動生成（`wiki/gee-copilot.html`）**：研究如何設計結構化 Prompt 讓 LLM 自動生成 GEE Python 遙測分析腳本（以新竹市 Sentinel-2 NDVI 分析為例），並規劃結合官方 API 文件 RAG 降低程式碼幻覺。
3. **無人機邊緣車流追蹤與 TWD97 映射（`wiki/yolo-deepsort.html`）**：整合 YOLOv8n-visdrone、DeepSORT 與共線方程式，將 UAV 影像中的交通軌跡即時映射至台灣 TWD97 平面座標系統。
4. **光達（LiDAR）操作手冊與法規 RAG 系統（`wiki/lidar-rag.html`）**：將點雲處理手冊、儀器操作規範與測量法規進行結構化切片與混合檢索（Embedding + BM25），建置可精準溯源頁碼的 RAG 檢索增強系統。

## 雙軌運作模式
- **資料儲存與編譯**：所有貼入的文章先存入 `raw/`（唯讀），經編譯後更新 `wiki/*.md` 與 `wiki/index.md`、`wiki/log.md`。
- **網頁展示**：同步依 [AGENTS.md](../AGENTS.md) 規範產出 Tailwind CSS 靜態 HTML 頁面並更新全站側邊欄導覽列。
