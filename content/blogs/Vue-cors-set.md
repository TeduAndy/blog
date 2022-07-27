---
title: VUE 前端與後端交互 cors \ 上線時 根目錄修改方式
date: 2022-07-21 11:39:35
categories: vue 
---


## <font color='#e59911'>1. CORS:</font>

#### **<font color='red'>說明:</font>**

**在以往前後端分離時 不同域名 或者 同域名但是不同PORT號 都會遇上 cors 跨域的問題, 一般都會在 後端 設定 cors 允許那些域名是可以進行訪問的,**

   **但是前端設置時必須一個一個針對有寫到 ajax 的部分 url 修改, 上線時域名也會不同 , 這時候還是要在修改一次, 相當麻煩, vue 這邊 提供前端設定**

   **cors 的方法, 並且可以針對後端的 url 取匿名 ,簡短對 ajax 使用時要填上完整的 url, 如果遇到 後端 域名換了只要修改配置文件那邊寫的後端url就**

   **可以修改全部有 ajax 有寫到url 的地方.**

<br>

#### **<font color='red'>使用方法:</font>**

+ **在 vite.config.js 配置文件裡面 的 export default defineConfig 添加這段 便可以使用 .**
**(/api 這寫法 路由會自帶 api , 不用的話用 rewrite 處理)**
```js
server: {
    proxy: {
      '/api': {
        target: 'https://localhost:7181/',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''), // 替換 /api 換成 空的
        secure: false
      }
    }
  }
```

<br>

## <font color='#e59911'>2. base 上線時 根目錄可能在某個資料夾時 根路徑修改</font>

#### **<font color='red'>說明:</font>**

**上線時 檔案全部是放在 某個資料夾底下, 也就是說路徑原本是 [https://localhost:3000/](https://localhost:44355/) 預設的根目錄是在自己目錄底下自動會自己找index.html,**

   **但是上線時 路徑 是會放在某個資料夾底下, 也就是說根目錄不是在自己的專案, 而是一個資料夾底下分門別類放著其他人的專案, 為了對應到自己的資料夾則需要另外在配置。**

<br>

#### **<font color='red'>使用方法:</font>**

+ **在 vite.config.js 配置文件裡面 的 export default defineConfig 添加這段 base: “路徑位置” ,便可以使用。**
```js
{
	base: '/ORD/ORDW1030/app',
	plugins: [vue()],
}
```