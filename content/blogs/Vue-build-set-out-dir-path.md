---
title: VUE build 打包輸出修改位置
date: 2022-07-21 14:03:30
categories: vue
---


### <font color='red'>說明:</font>

+ **輸出時 打包位置 改去別的地方**

<br>

### <font color='red'>使用方法:</font>

+ **在 vite.config.js 配置文件裡面 的 export default defineConfig 添加這段 build:{outDir: '輸出的位置路徑'},  打包時位置便會到輸入的路徑裡面**

```js
{
	build:{outDir: '../covid-19/covid-19/wwwRoot/app'}, // 配合輸出到 asp.net core 的 wwwRoot資料下底下
	plugins: [vue()],
}
```