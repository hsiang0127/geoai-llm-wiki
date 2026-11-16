# GEE Copilot：利用大語言模型自動生成遙測分析腳本（原始草稿）

- **來源類型**：使用者提供技術筆記草稿
- **保存日期**：2026-11-16

---

標題：GEE Copilot：利用大語言模型自動生成遙測分析腳本

概念簡介：
Google Earth Engine (GEE) 是空間資訊領域最常用的雲端運算平台，但其專屬的 JavaScript/Python API 學習門檻較高。透過結合大型語言模型 (LLM)，我們可以透過自然語言描述遙測需求，讓 AI 自動生成對應的 GEE 程式碼，大幅降低空間分析的技術壁壘。

應用情境：新竹市植被覆蓋度 (NDVI) 分析
傳統上，要篩選無雲的 Sentinel-2 影像並計算 NDVI，需要撰寫數十行程式碼。現在，我們只需輸入 Prompt：「請幫我寫一段 GEE Python 程式碼，篩選 2026 年新竹市區域雲量低於 10% 的 Sentinel-2 影像，計算 NDVI，並將結果輸出為 GeoTIFF。」

生成的程式碼範例：
```python
import ee
ee.Initialize()

# 定義目標區域 (新竹市)
hsinchu = ee.FeatureCollection("FAO/GAUL/2015/level2").filter(ee.Filter.eq('ADM2_NAME', 'Hsinchu City'))

# 篩選 Sentinel-2 影像並計算 NDVI
def addNDVI(image):
    ndvi = image.normalizedDifference(['B8', 'B4']).rename('NDVI')
    return image.addBands(ndvi)

collection = (ee.ImageCollection('COPERNICUS/S2_SR')
              .filterBounds(hsinchu)
              .filterDate('2026-01-01', '2026-12-31')
              .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10))
              .map(addNDVI))

# 取得中位數影像並裁剪
median_ndvi = collection.select('NDVI').median().clip(hsinchu)
print("NDVI 計算完成，準備匯出...")
```

未來展望：
未來可以將 GEE API 文件匯入 RAG (檢索增強生成) 系統，讓 LLM 在生成程式碼時能參考最新版本的 API 函數，減少幻覺 (Hallucination) 導致的編譯錯誤。
