# GeoAI 實戰：基於 YOLOv8 與 DeepSORT 的無人機車流追蹤與座標映射（原始文章）

- **來源類型**：使用者提供技術文章
- **保存日期**：2026-11-16

---

標題：GeoAI 實戰：基於 YOLOv8 與 DeepSORT 的無人機車流追蹤與座標映射

核心概念簡介：
隨著無人機 (UAV) 具備高機動性與廣闊視野的優勢，將其應用於城市交通監控與車流分析已成為 GeoAI 的熱門研究方向。本篇筆記將探討如何結合先進的電腦視覺物件偵測模型 (YOLOv8)、多目標追蹤演算法 (DeepSORT)，以及空間測量技術，將無人機二維影像中的車輛軌跡，精準映射至台灣真實的 TWD97 空間座標系統中。

技術架構與運作流程：
一套自動化的 UAV 邊緣運算車流偵測系統，主要由以下三個核心模組構成：

影像物件偵測 (Object Detection)
採用 YOLOv8n-visdrone 輕量化模型。該模型專門針對無人機俯視角、小目標物件（如遠處的車輛、行人）進行預訓練，能在運算資源受限的邊緣運算裝置上，保持高幀率 (FPS) 與高準確度。

多目標追蹤 (Multi-Object Tracking)
偵測到車輛後，系統引入 DeepSORT 演算法。DeepSORT 利用 ResNet50 卷積神經網路提取每輛車的外觀特徵 (Feature Extraction)，並結合卡爾曼濾波器 (Kalman Filter) 預測車輛的運動軌跡。這解決了車輛在行駛過程中被路樹遮蔽、或兩車交會時發生的 ID 丟失與錯置問題。

空間座標轉換 (Spatial Coordinate Mapping)
這是將純資訊工程轉化為空間資訊工程 (Geoinformatics) 的關鍵一步。透過相機內外參矩陣 (Camera Intrinsics & Extrinsics) 與無人機飛控系統紀錄的姿態數據 (Pitch, Roll, Yaw) 及 GPS 座標，我們能建立共線方程式，將畫面中追蹤到的每一幀車輛像素座標 (Pixel Coordinates)，映射至對應的 TWD97 二維平面座標。

核心程式碼範例 (Python 推理迴圈)：
```python
import cv2
import numpy as np
from ultralytics import YOLO
from deep_sort_realtime.deepsort_tracker import DeepSort

# 1. 載入無人機專用 YOLOv8 模型與設定 DeepSORT
model = YOLO('yolov8n-visdrone.pt')
tracker = DeepSort(max_age=30, n_init=3, nn_budget=100)

# 2. 開啟無人機影像串流
cap = cv2.VideoCapture('uav_traffic_video.mp4')

while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break

    # 3. YOLOv8 物件偵測
    results = model(frame)[0]
    detections = []
    
    for box in results.boxes:
        x1, y1, x2, y2 = box.xyxy[0].tolist()
        conf = box.conf[0].item()
        cls_id = int(box.cls[0].item())
        
        # 篩選車輛類別 (假設 2, 3, 5, 7 為各類車輛)
        if cls_id in [2, 3, 5, 7] and conf > 0.5:
            # 轉換為 DeepSORT 所需格式 [left, top, w, h]
            detections.append(([x1, y1, x2 - x1, y2 - y1], conf, cls_id))

    # 4. DeepSORT 軌跡追蹤
    tracks = tracker.update_tracks(detections, frame=frame)
    
    for track in tracks:
        if not track.is_confirmed():
            continue
        
        track_id = track.track_id
        ltrb = track.to_ltrb() # [left, top, right, bottom]
        
        # 計算車輛底盤中心點 (Pixel Coordinate)
        center_x = int((ltrb[0] + ltrb[2]) / 2)
        center_y = int(ltrb[3])
        
        # TODO: 將 (center_x, center_y) 透過轉換矩陣映射至 TWD97 座標
        # twd97_x, twd97_y = pixel_to_twd97(center_x, center_y, drone_telemetry)
        
        # 繪製追蹤框與 ID
        cv2.rectangle(frame, (int(ltrb[0]), int(ltrb[1])), (int(ltrb[2]), int(ltrb[3])), (0, 255, 0), 2)
        cv2.putText(frame, f"ID: {track_id}", (int(ltrb[0]), int(ltrb[1]) - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.6, (0, 255, 0), 2)

    cv2.imshow('UAV Traffic Tracking', frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

未來應用展望：
透過這套系統即時產生的 TWD97 座標軌跡，我們不僅能計算各路段的真實車速、車流密度，還能將軌跡資料直接匯入 QGIS 或 ArcGIS Pro 進行空間熱區分析。結合邊緣運算平台，無人機將具備在災區、特殊路段即時回傳交通數據的能力，大幅提升智慧城市的交通治理效率。
