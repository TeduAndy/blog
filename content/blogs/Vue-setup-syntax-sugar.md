---
title: VUE3 語法糖
date: 2022-07-21 14:16:42
categories: VUE
---

### <font color='e59911'>1. Vue3 的一大特性函数 ---- setup</font>
+ **說明: setup函数是 Composition API（组合API）的入口**

<br>

### <font color='e59911'>2. data 輸出到 Template 採用兩種函數</font>

+ **<font color='e59911'>1. ref函数 (使用常量居多)</font>**

	**ref 是一个函数，它接受一个参数，返回的就是一个神奇的 响应式对象 。我们初始化的这个 0 作为参数包裹到这个对象中去**
	**，在未来可以检测到改变并作出对应的相应**
```js
<script setup lang="ts">
	const name = ref("123")
</script>
```

<br>

+ **<font color='e59911'>2. reactive函数 (使用物件為主)</font>**
	**使用 ref 还是 reactive 可以选择这样的准则**
	**第一，就像刚才的原生 javascript 的代码一样，像你平常写普通的 js 代码选择原始类型和对象类型一样来选> 择是使用 ref 还是 reactive。**

	**第二，所有场景都使用 reactive，但是要记得使用 toRefs 保证 reactive 对象属性保持响应性。**
```js
<script setup lang="ts">
const name = reactive({
                        name:"123",
                        age:20
                     })
</script>
```

<br>

### <font color='e59911'>3. 生命週期鉤子</font>

+ **vue2 跟 vue3 對應**

|<font color='e59911'>vue2</font>|<font color='e59911'>vue3</font>|
|   :----------:    |    :----------:     |
|**beforeCreate**   |                     |
|**created**        |                     |
|**beforeMount**    |**onBeforeMount**    |
|**mounted**        |**onMounted**        |
|**beforeUpdate**   |**onBeforeUpdate**   |
|**updated**        |**onUpdated**        |
|**beforeUnmount**  |**onBeforeUnmount**  |
|**unmounted**      |**onUnmounted**      |
|**errorCaptured**  |**onErrorCaptured**  |
|**renderTracked**  |**onRenderTracked**  |
|**renderTriggered**|**onRenderTriggered**|
|**activated**      |**onActivated**      |
|**deactivated**    |**onDeactivated**    |

<br>

```js
<script setup lang="ts">
	onMounted(() => {
		console.log('Component is mounted!')
	})
</script>
```


