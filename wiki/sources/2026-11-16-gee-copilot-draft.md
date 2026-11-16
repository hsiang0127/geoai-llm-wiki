---
title: "GEE Copilot：利用大語言模型自動生成遙測分析腳本（草稿摘要）"
type: source
tags:
  - geoai
  - gee
  - copilot
  - ndvi
  - sentinel-2
created: 2026-11-16
updated: 2026-11-16
published: 2026-11-16
authors: "使用者筆記草稿"
raw_path: "raw/articles/2026-11-16-gee-copilot-draft.md"
status: evergreen
---

# GEE Copilot：利用大語言模型自動生成遙測分析腳本

## 一句話核心結論（TL;DR）
利用大型語言模型（LLM）將自然語言遙測需求直接轉譯為 Google Earth Engine（GEE）Python 程式碼，可大幅降低空間運算 API 學習門檻；未來結合 GEE API 文件的 RAG 系統可進一步抑制版本過時與函數幻覺。

## 應用情境與實作重點
- **案例區域**：新竹市（Hsinchu City）2026 年 Sentinel-2 影像。
- **篩選條件**：雲量比例 `< 10%`（`CLOUDY_PIXEL_PERCENTAGE`）。
- **指標運算**：使用近紅外（`B8`）與紅光（`B4`）波段計算常態化差異植生指標（NDVI），並取年度中位數合成與邊界裁剪。

## 工程檢核與後續優化建議
- **資料集版本提醒**：原草稿使用 `COPERNICUS/S2_SR`，實務執行時建議改用 GEE 官方維護中的 `COPERNICUS/S2_SR_HARMONIZED` 以避免棄用警告或波段偏移差異。
- **邊界名稱確認**：使用 `FAO/GAUL/2015/level2` 篩選台灣行政區時，需實際確認該縣市在 `ADM1_NAME` / `ADM2_NAME` 中的英文拼寫屬性，或改用更精確的台灣國土測繪中心行政區界圖資（匯入 GEE Asset）。
- **GeoTIFF 匯出步驟**：範例程式已取得 `median_ndvi`，若要完成匯出至 Google Drive，需補上 `ee.batch.Export.image.toDrive(...)` 與 `.start()`。

## 關聯的 Wiki 頁面
- 概念：[[gee-copilot-prompt-generation]]
- 總覽：[[overview]]
- 網頁實作：`wiki/gee-copilot.html`
