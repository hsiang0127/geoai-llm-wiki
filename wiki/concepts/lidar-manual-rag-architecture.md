---
title: "光達操作手冊與測量法規 RAG 檢索架構（LiDAR Manual & Regulation RAG）"
type: concept
tags:
  - geoai
  - lidar
  - rag
  - hybrid-search
  - las-1-4
created: 2026-11-16
updated: 2026-11-16
status: growing
sources: []
---

# 光達操作手冊與測量法規 RAG 檢索架構

> 對應網頁筆記：[lidar-rag.html](../lidar-rag.html)

## 核心問題
光達（TLS / ALS / UAV-LiDAR）儀器手冊與測繪規範包含大量精密數值門檻（航高、重疊率、IMU 校準週期、RMSEz 檢核容許值、LAS 1.4 屬性與 TWD97 / TWVD2001 基準），通用 LLM 容易產生參數幻覺。

## 三段式解決架構
1. **結構化切片（Structure-Aware Chunking）**：保留規格表格與章節頁碼 Metadata（`doc_name`、`device_model`、`section`、`page`）。
2. **混合檢索（Hybrid Search）**：結合 Embedding 語意檢索與 BM25 精確詞彙匹配（確保型號、錯誤碼、法規條號與縮寫如 PDOP、RTK 命中）。
3. **強制溯源輸出（Citation-Grounded Generation）**：透過 Prompt 約束每個關鍵參數必須標註文件名稱與頁碼，未收錄則拒答。

## 相關連結
- 與 [[gee-copilot-prompt-generation]] 共用抗幻覺 RAG 檢索基礎架構
- 總覽：[[overview]]
- 網頁實作：`wiki/lidar-rag.html`
