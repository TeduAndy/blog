---
title: VUE3 compontent $emit 和 emits 說明及設置
date: 2022-10-01 14:16:42
categories: vue
---

### <font color='e59911'>Vue3 Compontent emit emits</font>

<br>

#### 說明：組件封裝了多個 emit 事件，回傳數據或者回調函數等等，外部使用時採用 @設置的emit名稱="自己配置的方法"，從而讓 compontent 應用 外部的方法。

<br>

#### emits：設置組件自定義的事件名稱，設置時可以是 Array 或 Object 寫法如下
```js
<script>
	// 此寫法是 cdn 使用
	const compontent1 = {
		template: `<button @click="this.$emit('MeClick')">com</button>`,
		emits: ["MeClick"],
		props: ["prop"],
	};

	// 在 vite 或者 cli 則是
	
	// Array 寫法
	const emit = defineEmits(['change', 'delete'])
	
	// Object 寫法
	const emit = defineEmits({
		change:()=>{},
		delete:()=>{}
	})
</script>
```

<br>

#### $emit：觸發當前實際例子上的事件，附加參數也會帶進來，第一個為組件自定義名稱並且會帶入在父組件在自定義名稱裡面寫的方法或者其他，第二個跟第三個...之後都是傳給綁定的參數
```js
<script setup>
	this.$emit('自定義的名稱', 參數1, 參數2)
</script>
```

<br>
<br>
<br>

#### 實際例子如下(採用cdn作為例子)：
#### 會發現內部配置的 MeClick 使用的方法是外部的 newclick 事件
```js
<body>
	<div id="app">
		<div>
			<btn @Me-Click="newclick()"></btn>
		</div>
	</div>
</body>
<script src="https://unpkg.com/vue@next"></script>
<script>
	const { ref, createApp, emits, $emit } = Vue;
	const compontent1 = {
	template: `<button @click="this.$emit('MeClick')">com</button>`,
	emits: ["MeClick"],
	};

	createApp({
	setup() {
		const newclick = () => {
		alert(123);
		};
		return {
		newclick,
		};
	},
	})
	.component("btn", compontent1)
	.mount("#app");
</script>
```

