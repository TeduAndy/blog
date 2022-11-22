---
title: AXIOS 基礎用法及夾帶JWT-Bearer_Token
date: 2022-11-20 15:13:32
categories: JavaScript
---


### **AXIOS 說明：**
- 一個前端輕量型的 httpclient
- 可以發送 http 請求
- 攔截響應跟請求
- 自動轉換成 json 格式
- 支持 Promise 

<br>

### **應用場景：**
- 分離式專案時需要向後端索取資料
- 跟不同 API 界接時使用

<br>

### **安裝方法**
- npm 安裝方法
```cmd
npm install axios
```
- cdn 直接引入
```js
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

<br>

### **使用方法**

<br>

#### 1. 基本寫法 以及 夾帶token
```js
// 引入 axios 之後

// GET
axios({ method: 'GET', 
		url: 'url', 
		data: { 
		param1: 'param1', 
		param2: 'param2' 
		} });

// POST 用法
axios({ method: 'post', 
		url: 'url',
		headers: {
          'Content-Type': 'application/json', 
		  'Authorization': `Bearer ${token}` 
      	}, 
		data: { 
		param1: 'param1', 
		param2: 'param2' 
		} });
```

#### 2. get、post 以及 夾帶token
```js
// GET
const configGet = {
	params:{
		key:value
	},
	 headers: {
		'Content-Type': 'application/json', 
		'Authorization': `Bearer ${token}` 
	}
}

axios.get('url',configGet)


// POST
const data = {key: value} // params
const configPost = {
	headers: {
	  'Content-Type': 'application/json',
      'Authorization': `Bearer ${token}` 
    }
}
axios.get('url',data, configPost)
``` 