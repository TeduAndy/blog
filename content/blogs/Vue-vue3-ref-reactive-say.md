---
title: VUE3 ref、reactive說明 
date: 2022-10-01 14:16:42
categories: vue
---

### <font color='e59911'>Vue3 雙向綁定用到的函數 ref 跟 reactive 區別</font>

<br>

#### 1. 說明：
-  **ref： 接收任何型態的資料放入，但是不會對每一個元素都進行監聽，Object 和 Array 裡面的元素也不會監聽，取值方式須使用 .value 進行取值。**

<br>

- **reactive： 只接受 Array 跟 Object 能夠放入，並且會針對每一個元素進行監聽，同時還不需要使用 .value 去獲得值。**

<br>

#### 實際例子：

```js
<script lang='ts' setup>
	import { watch, reactive, ref  } from "vue";

	const exampleRef = ref({number: 0})
	const exampleReactive = reactive({number: 0})

	// 取值方式說明 ref 部分
	exampleRef.value // 才能取出放入的物件或者其他資料類型
	exampleRef.value.number // 才能取出在物件裡面的元素

	// 取值方式說明 reactive 部分，這邊取值就不需要再使用 .value
	exampleReactive.number // 直接向物件取值方式一樣，Array則是使用索引

	// 底下這邊實際測試監聽狀態
	watch(exampleRef, (newValue)=>{
		console.log(newValue)
	})

	watch(exampleReactive, (newValue)=>{
		console.log(newValue)
	})

	// 設置時間讓值修改
	setTimeout(() => {
		exampleRef.value.number = 1
		exampleReactive.number = 1
	}, 5000);
</script>
```

<br>

#### 2. 說明：
- **藉由上面的範例會發現一件事情，當值改變的時候，ref 並未執行 ，reactive 卻執行。**
<br>
- **ref 雖然 Object 裡面的值改變了，但是它本身還是 Object，對於它而言型態還未修改就不會執行。**
<br>
- **reactive 則是同時也會對 Object 或 Array裡面的值進行監聽，所以遇到值改變，監聽事件馬上就會觸發**

