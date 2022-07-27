---
title: Hexo 分類設定
date: 2022-07-19 16:08:18
categories: Blog-Hexo框架
---

### **如何使用categories進行分類**
+ **1. 第一步驟先到bash下指令新增分類**
```bash
hexo new page category
```
+ **2. 會發現 主目錄的 source資料夾底下多了一個 category資料夾，點開裡面的 index.md**
```md
title: 分類 // 類別頁面的標題
date: 2022-07-15 11:35:52
type: category // 型態可以自己取
layout: "category" // 版面呈現 用於 你在使用的樣式專案
```
+ **3. 接下來到需要分類的 md文檔 進行設定**
```md
title: 文檔標題名稱
date: 時間
category: Hexo // 這個 category 是你在 type 設置的名字 用來判別是用於分類，後面的 Hexo 則是 你分類頁面 會顯示有一個分類區塊叫做 Hexo ，文檔裡面設置是這個名字的都會被歸類在Hexo底下。
```

<br>

### **接下是切換到樣式專案裡面的 _config.yml 裡面設置**
+ **找尋 nav 或者 menu 的設置，把**
```
nav:
# Resume:
Posts: /archives
# category: /category     // 把#字號刪除 就打開了
```
+ **設置好後，在啟動伺服器時要先清除舊的靜態資源，然後生成新的靜態支援後再啟動**
```bash
hexo clean // 先把原來的靜態資源清空
hexo generate // 再重新生成新的靜態資源
hexo server // 再執行 模擬伺服器，這對之後做分類頁面很重要
```