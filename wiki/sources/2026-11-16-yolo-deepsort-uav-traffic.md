---
title: "GeoAI 實戰：基於 YOLOv8 與 DeepSORT 的無人機車流追蹤與座標映射（來源摘要）"
type: source
tags:
  - geoai
  - uav
  - yolov8
  - deepsort
  - twd97
created: 2026-11-16
updated: 2026-11-16
published: 2026-11-16
authors: "使用者提供技術文章"
raw_path: "raw/articles/2026-11-16-yolo-deepsort-uav-traffic.md"
status: evergreen
---

# GeoAI 實戰：基於 YOLOv8 與 DeepSORT 的無人機車流追蹤與座標映射

## 一句話核心結論（TL;DR）
整合針對無人機俯視角訓練的輕量偵測模型（`YOLOv8n-visdrone`）、外觀與運動特徵追蹤演算法（DeepSORT），以及基於共線方程式的空間座標轉換管線，可將二維 UAV 影像中的車輛軌跡即時映射至台灣 **TWD97** 平面座標系統，供 QGIS / ArcGIS Pro 進行車速與熱區分析。

## 核心架構模組
1. **影像物件偵測**：`YOLOv8n-visdrone`，兼顧俯視小目標偵測與邊緣裝置高 FPS 需求。
2. **多目標追蹤**：DeepSORT 結合 ResNet50 外觀特徵萃取與卡爾曼濾波器，降低路樹遮蔽與車輛交會導致的 ID Switch。
3. **空間座標轉換**：結合相機內外參矩陣、飛控姿態（Pitch / Roll / Yaw）與 GPS 座標建立共線方程式，將車輛底盤中心像素座標（`(center_x, center_y)`）轉為 TWD97 座標。

## 實務註記
- 範例程式碼中，VisDrone 預訓練權重類別編號與 COCO（`2, 3, 5, 7`）可能不同，實作部署時需確認模型 `model.names` 映射表。
- 共線方程式單應性／地形投影在道路坡度明顯處，建議搭配 DSM 高程迭代求解以提升 TWD97 映射精度。

## 關聯的 Wiki 頁面
- 概念：[[uav-traffic-tracking-twd97]]
- 關聯筆記：[[uav-multimodal-thickness-estimation]]
- 網頁實作：`wiki/yolo-deepsort.html`
