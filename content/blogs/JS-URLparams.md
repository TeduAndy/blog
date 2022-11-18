---
title: JS 路由參數解析(URL Parameters)
date: 2022-07-19 13:47:37
categories: JavaScript
---

### **說明：**
- **大部分路由解析都是透過 location.href 然後下去判斷分解取出 Param 的參數**
- **這邊可以使用瀏覽器內建的 URL API 去做解析，獲得 Paramter 參數**

<br>

### **教學(URL 介紹)**
```JS
// 創建一個URL物件
const param = new URL("路由網址");

// 獲取完整路由
param.href;

// 取得網址中的主機名稱
param.hostname; 

// 取得網頁路徑部分
param.pathname; 

// 取得網址中的通訊協定部分
param.protocol; 

// 取得網頁參數部分
param.search; 
param.searchParams; 
```

<br>

### **實際例子**
```JS
const param = new URL("https://www.google.com.tw/?hl=zh_TW")

param.href // https://www.google.com.tw/?hl=zh_TW

param.hostname // www.google.com.tw

param.protocol // https

param.search //?hl=zh_TW

param.searchParams; // URLSearchParams {}
```

<br>

### **searchParams 會將 參數包成物件，並且可以用 key value 去獲取值**
#### **例子**
```JS
// 套用上面範例已經創建好物件 可以使用searchParams的方法 get、has 兩個

// has 是判斷 參數是否有這個 key
const paramOj = param.searchParams
paramOj.has('hl') // true
paramOj.get('hl') // zh_Tw
```

