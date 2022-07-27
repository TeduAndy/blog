---
title: Hexo 安裝 及 設置
date: 2022-07-19 15:01:23
categories: Blog-Hexo框架
---

### 1.安裝 Hexo  
+ **（電腦必須先安裝 git 和 node.js）**

```bash
npm install -g hexo-cli
```

<br>

### 2.建立 Hexo 專案
+ **1.產生一個叫做 blog 的資料夾，資料夾名稱可以任意更改，必須是英文**

```bash
hexo init blog
```
+ **2.切換到創建的blog專案裡面，並且用npm安裝hexo必需的套件**
```bash
cd blog

npm install
```
+ **3.輸入底下指令在本地端開啟測試伺服器，預設 port 號 是 4000 ， 在網址輸入：http://localhost:4000/ 即可預設網頁**
```bash
hexo server
```

<br>

### 3.Hexo 設定

+ **Hexo 專案結構**

```
├── source // markdown檔案放置位置
|   ├── _drafts
|   └── _posts
├── _config.yml // 參數設置
├── package.json // node_modules 須安裝的東西
├── scaffolds
└── themes // 下載樣式存放位置
```

<br>

### 4.Hexo 樣式下載 及 設定
+ **1. 樣式下載可以到 Hexo官網 [樣式下載](https://hexo.io/themes/)這邊找，然後點選樣式進入樣式裡面的 gtihub，下載樣式的專案 放到 自己專案 themes資料夾 底下**
```
├── _config.yml // 參數設置
└── themes // 下載樣式存放位置
	└── hexo-theme-Chic  // 這個是 下載下來的樣式名稱
```
+ **2. 然後到 主目錄裡面的 _config.yml 找到一個 theme 進行樣式設置**
```
theme: hexo-theme-Chic // 修改成 你想轉換的樣式專案名稱
```
+ **3. 重新啟動，這邊重新啟動有一個重點，須先將原本生成的靜態資源刪除，創新的之後再執行伺服器**
```bash
hexo clean // 先把原來的靜態資源清空
hexo generate // 再重新生成新的靜態資源
hexo server // 再執行 模擬伺服器，這對之後做分類頁面很重要
```

<br>

### 4.指令新增文章
```bash
hexo new post "文章名稱"
```
+ **輸入完後會在 source資料夾底下的 _posts資料夾底下多出一個 創建的文章名稱的.md檔案**
```
source
└── _posts
	└── 文章名稱.md
```
+ **該md文檔基本配置**
```
---
title: 文章名稱
date: 2022-07-19 16:30:00
tags:
---
```
