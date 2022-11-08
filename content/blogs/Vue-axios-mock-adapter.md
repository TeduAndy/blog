---
title: axios-mock-adapter為axios提供測試用的假資料
date: 2022-07-21 15:01:51
categories: VUE
---

### <font color='e59911'>安裝指令:</font>
```bash
npm install axios-mock-adapter --save-dev
```

<br>

### <font color='e59911'>說明:</font>
   **開發時期或是要做Unit testing需要用假資料來取代server api直接回傳。**
```js
import axios from 'axios'
import MockAdapter from 'axios-mock-adapter'

let mock = new MockAdapter(axios)

mock.onGet('/users').reply(200, {
  users: [
    { id: 1, name: 'John Smith' },
    { id: 2, name: 'John Doe' }
  ]
})

axios.get('/users')
  .then(response => {
    console.log(response.data)
  })
```

<br>

### <font color='e59911'>使用方法:</font>
   **創建uri跟假資料的對應很簡單, 基本上也就是’on'‘Method’, 比如說`onGet`, `onPost`, 另外還有一個`onAny`可以處理所有的HTTP methods**
   **做過mock後, axios呼叫這個uri所拿回來的資料通通就都會是假資料了, 這樣也不用為了塞假資料開發測試而去改動自己的程式**



