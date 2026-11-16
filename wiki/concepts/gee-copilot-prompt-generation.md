---
title: "GEE Copilot 與遙測程式碼生成（GEE Copilot & Prompt-to-Code）"
type: concept
tags:
  - geoai
  - gee
  - prompt-engineering
  - rag
  - sentinel-2
created: 2026-11-16
updated: 2026-11-16
status: growing
sources:
  - "[[2026-11-16-gee-copilot-draft]]"
---

# GEE Copilot 與遙測程式碼生成

> 對應網頁筆記：[gee-copilot.html](../gee-copilot.html)

## 定義與核心直覺
Google Earth Engine（GEE）具備強大的雲端遙測運算能力，但使用者必須熟悉其伺服器端物件模型（`ee.Image`、`ee.ImageCollection`、`ee.Filter` 與 `.map()` 映射語法）。透過 **Prompt Engineering**，LLM 可扮演「GEE Copilot」，將自然語言分析流程自動編譯為可執行的 Python 或 JavaScript 遙測腳本。

## 典型 Prompt 設計要素
一個高品質的 GEE 生成 Prompt 通常需明確給定五項約束條件：
1. **語言與 SDK**：指定 Python API（`import ee`）或 Code Editor JavaScript。
2. **時空範圍**：明確的起訖日期（如 `2026-01-01` 至 `2026-12-31`）與行政區界／座標邊界。
3. **衛星資料集與過濾條件**：如 Sentinel-2 地表反射率資料集與雲量閾值（`< 10%`）。
4. **波段運算與合成方式**：如 `normalizedDifference(['B8', 'B4'])` 計算 NDVI 並取中位數（`.median()`）。
5. **輸出格式**：如 GeoTIFF 匯出設定。

## 常見問題與 RAG 結合展望
- **API 幻覺與資料集棄用**：LLM 訓練資料可能停留在舊版寫法（例如仍輸出舊的 `COPERNICUS/S2_SR` 而非 `S2_SR_HARMONIZED`，或捏造不存在的波段名稱）。
- **解方**：將最新的 GEE 官方 API 文件、Data Catalog 清單與範例腳本納入 **RAG（檢索增強生成）** 索引（可與 [[overview]] 中規劃的 `lidar-rag.html` 共用 RAG 檢索架構），在程式碼生成前先檢索最新函數簽章。

## 相關連結
- 來源依據：[[2026-11-16-gee-copilot-draft]]
- 關聯概念：[[uav-multimodal-thickness-estimation]]
- 網頁實作：`wiki/gee-copilot.html`
