---
title: "無人機多模態影像厚度與空間尺度推算（UAV Multimodal Scale & Thickness Estimation）"
type: concept
tags:
  - geoai
  - uav
  - vlm
  - gemini-vision
created: 2026-11-16
updated: 2026-11-16
status: seed
sources: []
---

# 無人機多模態影像厚度與空間尺度推算

> 對應網頁筆記：[uav-vision.html](../uav-vision.html)（測試範例）

## 核心概念
單張無人機 RGB 影像缺乏絕對深度資訊，不能直接要求多模態視覺語言模型（VLM，如 Gemini Pro Vision）憑空猜測公分或公尺級尺寸。正確的 GeoAI 工程做法是將**空間幾何約束**納入 Prompt：
1. 讀取無人機 **EXIF / GNSS** 航高與相機參數推算 **GSD（地面採樣距離）**，或放置已知邊長的現場校正標靶（如 AprilTag / 標準色卡）。
2. 結合低空斜拍視角（Oblique View，約 30°～45°）與陰影邊緣線索，作為厚度與高度的視覺比例線索。
3. 透過結構化 Prompt Engineering 強制輸出 JSON Schema（包含 `estimated_thickness_cm`、`coverage_area_m2`、`confidence` 與 `reasoning`）。

## 實務限制與演進方向
- 僅依賴氣壓計相對航高估算 GSD 時，遇到明顯地形起伏容易出現 5%～15% 尺度誤差。
- 高精度測量應先透過多視角影像重建 **DSM（數值表面模型）**，再交由 VLM 執行語意區域分割與體積統計。

## 相關連結
- [[overview|GeoAI 研究總覽]]
- 網頁實作：`wiki/uav-vision.html`（含 Python / Gradio 驗證介面原型）
