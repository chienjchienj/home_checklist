# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 本地開發

無需建置工具，直接用 HTTP server 啟動：

```bash
python3 -m http.server 8080
# 或
npx serve .
```

部署只需 push 到 main，GitHub Pages 約 1~2 分鐘自動更新。

線上網址：https://chienjchienj.github.io/home_checklist/

## 架構

整個 app 是**單一 `index.html` 檔案**，無任何框架或建置步驟。

- `index.html` — 全部 UI、CSS、JavaScript 都在這裡
- `manifest.json` — PWA 設定（icon、顯示模式）
- `sw.js` — Service Worker，快取 `index.html` 和 `manifest.json` 實現離線功能

資料全部存在 `localStorage`，共三個 key：
- `checklist-items-v1` — 任務清單（icon + text）
- `checklist-done-v1` — 每天勾選狀態（以日期為 key）
- `checklist-history-v1` — 歷史紀錄（最近 30 天）

## 重要設計細節

**iOS 觸控相容**：所有按鈕互動使用自訂的 `tap()` 函式，同時綁 `touchend` 和 `click`，並過濾滑動手勢（位移超過 8px 不觸發）。直接用 `addEventListener('click')` 在 iOS Safari 上會有延遲或失效問題。

**滑動解鎖任務**：未完成的任務需滑動 check-circle 至 60% 寬度才觸發完成，用 `touch-action: none` 在 handle 上防止與頁面捲動衝突。

**編輯模式密碼**：密碼寫死在 JS 頂部 `const PASSWORD = '1234'`。編輯模式透過 CSS class `.edit-mode` 切換，進入時 check-circle 的外觀必須覆蓋 `.done` 狀態（否則已完成任務會顯示綠色圓圈而非 emoji）。

**背景彩虹**：用 `body::after` 偽元素加 `radial-gradient` 實現，`body::before` 為彩色泡泡背景。兩者都是 `position: fixed`、`z-index: 0`，內容 `.app` 為 `z-index: 1`。

**Service Worker 版本**：更新 sw.js 的 `CACHE` 常數版本號（如 `v2`）才能讓使用者的瀏覽器清除舊快取。
