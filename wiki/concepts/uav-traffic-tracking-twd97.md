---
title: "無人機車流追蹤與 TWD97 空間座標映射（UAV Traffic Tracking & TWD97 Mapping）"
type: concept
tags:
  - geoai
  - uav
  - yolov8
  - deepsort
  - twd97
  - photogrammetry
created: 2026-11-16
updated: 2026-11-16
status: growing
sources:
  - "[[2026-11-16-yolo-deepsort-uav-traffic]]"
---

# 無人機車流追蹤與 TWD97 空間座標映射

> 對應網頁筆記：[yolo-deepsort.html](../yolo-deepsort.html)

## 核心概念與管線設計
將電腦視覺從「純像素框選」推進至「空間資訊工程（Geoinformatics）」的關鍵在於為每幀偵測結果賦予真實大地座標：
1. **偵測（YOLOv8n-visdrone）**：針對無人機俯視小目標最佳化，篩選感興趣車輛類別並轉為 `[left, top, w, h]` 格式。
2. **追蹤（DeepSORT）**：透過 ResNet50 外觀特徵與卡爾曼濾波維持跨幀 ID 一致性，並取底盤接地邊緣中心 `((left + right)/2, bottom)` 作為空間定位代表點（相較於框中心更貼近真實地面投影）。
3. **座標映射（共線方程式 / TWD97）**：利用相機內外參矩陣與飛控姿態（Pitch, Roll, Yaw）、GNSS 定位資訊，將影像像素座標映射至台灣 **TWD97** 平面座標系統。

## 與其他無人機筆記的關聯
- 與 [[uav-multimodal-thickness-estimation]] 互補：前者專注於透過 VLM 與空間比例尺進行低頻語意判釋與厚度推算；本主題則聚焦於高幀率邊緣推論（YOLOv8 + DeepSORT）與連續軌跡之地理坐標化。

## 相關連結
- 來源依據：[[2026-11-16-yolo-deepsort-uav-traffic]]
- 總覽：[[overview]]
- 網頁實作：`wiki/yolo-deepsort.html`
