# 🏠 回家任務清單

> 專為小朋友設計的每日回家任務 PWA，讓孩子養成放學後的好習慣！

🌐 **線上使用**：[https://chienjchienj.github.io/home_checklist/](https://chienjchienj.github.io/home_checklist/)

---

## 畫面預覽

| 主畫面 | 慶祝動畫 | 歷史紀錄 |
|--------|----------|----------|
| 進度條 + 任務卡片 | 全部完成時觸發紙屑 🎉 | 最近 30 天完成紀錄 |

---

## 功能介紹

### ✅ 任務勾選
- 點擊任務卡片即可勾選／取消
- 進度條即時更新，顯示完成百分比
- 全部完成後自動跳出慶祝動畫 + 紙屑特效

### ✏️ 編輯模式（密碼保護）
- 按「編輯」按鈕需輸入 **4 位數密碼**，防止孩子自己亂改
- 進入編輯模式後可以：
  - 新增任務（輸入名稱，自動隨機指派 emoji）
  - 刪除任務（點 ❌）

### 📅 歷史紀錄
- 自動記錄每天的完成狀況
- 保留最近 **30 天**紀錄
- 顯示每天完成項目數與詳細內容

### 🔄 每日重置
- 按「重置」可清空今天的勾選，重新開始

---

## 預設任務清單

| Emoji | 任務 |
|-------|------|
| 👟 | 換居家服 |
| 🍱 | 吃點心 |
| 📚 | 寫功課 |
| 🎒 | 整理書包 |
| 🛁 | 洗澡 |
| 😴 | 準備睡覺 |

---

## 安裝到 iPhone 主畫面（PWA）

1. 用 **Safari** 開啟 [https://chienjchienj.github.io/home_checklist/](https://chienjchienj.github.io/home_checklist/)
2. 點下方工具列的 **分享按鈕** `□↑`
3. 選擇「**加入主畫面**」
4. 點「新增」完成

安裝後可離線使用，體驗與原生 App 相同。

---

## 修改密碼

開啟 `index.html`，找到第一行設定：

```js
const PASSWORD = '1234';  // ← 改成你想要的 4 位數密碼
```

修改後存檔並推送到 GitHub 即可生效。

---

## 專案結構

```
home_checklist/
├── index.html      # 主程式（UI + 邏輯全在這裡）
├── manifest.json   # PWA 設定檔
├── sw.js           # Service Worker（離線快取）
├── icon-192.png    # App 圖示（192×192）
└── icon-512.png    # App 圖示（512×512）
```

---

## 技術說明

| 項目 | 說明 |
|------|------|
| 框架 | 純 HTML / CSS / JavaScript，無任何依賴 |
| 資料儲存 | `localStorage`（存在裝置本機） |
| 離線支援 | Service Worker 快取所有靜態資源 |
| 部署 | GitHub Pages |
| 字型 | [Nunito](https://fonts.google.com/specimen/Nunito)（Google Fonts） |
| iOS 相容 | `touchend` 事件處理，修正 Safari 點擊延遲問題 |

---

## 本地開發

不需要任何建置工具，直接用瀏覽器開啟即可：

```bash
git clone https://github.com/chienjchienj/home_checklist.git
cd home_checklist
# 用任意 HTTP server 啟動，例如：
npx serve .
# 或
python3 -m http.server 8080
```

> ⚠️ Service Worker 需要 `localhost` 或 `https` 環境才能正常運作，直接雙擊 `index.html` 開啟時 SW 不會啟用，但其他功能正常。

---

## 部署更新

```bash
git add .
git commit -m "your message"
git push
```

推送後約 1～2 分鐘，GitHub Pages 自動更新。

---

## License

MIT
