---
title: VUE axios 重新包裝
date: 2022-07-21 14:09:01
categories: VUE
---

#### <font color='e59911'>說明:</font>

**一般使用 axios 是 直接 import 引入 雖然 後端路由 可以透過 配置 重新命名處理掉一長串的網址**

  **但是 如果遇到了 根目錄位置不對的時候 還是要在重新命名的路由在加上之後的位置, 等於說 有使用到 axios 的都要改**

  **這邊 VUE 有提供 二次包裝 可以在 axios 被呼叫之前 增加裡面的配置 在被呼叫出來。**

<br>

#### <font color='e59911'>使用方法(先建立一個 js 檔案 並且加入以下):</font>
```js
// 先引入 原本安裝的 axios
import axios from "axios";

// 這邊設定 產生時 自帶的 url設定(baseURL), 設定頭部則是(headers)
const request = axios.create({
    baseURL: '/ORD/ORDW1030',
    headers: { 'Content-Type': 'application/json' },
  })

// 這邊是輸出這個設定好的 axios (別的地方引入時輸出甚麼東西給對方使用)
export default request

```

<br>

#### <font color='e59911'>別人引入使用:</font>
```js
import 自己重新命名 from 設定的 js檔案
```

