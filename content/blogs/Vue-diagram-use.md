---
title: VUE3 柱狀圖實現
date: 2022-07-21 15:13:32
categories: VUE
---


### **<font color='e59911' >說明：</font>**

**需要實現一些 數據上的顯示 網路上有許多框架，但是 HIHHCHARTS 框架較為方便設定**

<br>

### **<font color='e59911' >操作方法：</font>**

+ **1. 先在 VUE 專案裡面輸入指令安裝**
```bash
npm i --save vue3-highcharts
```

<br>

+ **2. 這邊不採用全域引入，使用需要再引入的方式**

**<font color='e59911' >template 設定</font>**
```html
<div class="col-md-8">
	<vue-highcharts
		type="chart"      <!-- 型態 -->
		:options="chartOptions"  <!-- 要綁入的參數都寫在這邊 -->
		:redrawOnUpdate="true"
		:oneToOneUpdate="false"
		:animateOnUpdate="true"
		style="width: auto"  <!-- 為了讓整體填充滿整個 div -->
	/>
</div>
```
**<font color='e59911' >script setp lang=”ts” 設定</font>**
```js
import VueHighcharts from "vue3-highcharts";   //  分批引入使用


// 每一個 data 的 數據
const seriesData = ref([40, 50, 45, 45, 50, 45]);
// 每一個 X 的 數據
const categories = ref([
  "Python",
  "JavaScript",
  "C#",
  "VUE",
  "Asp.net core",
  "Django",
]);

const chartOptions = {
	// 欄位顏色設定
  colors: ["#7cb5ec", "#434348", "#90ed7d", "#f7a35c", "#8085e9"],
	// 柱狀樣式 或者 其他樣式
  chart: {
    type: "column",
  },
  // 標題 
  title: {
    text: "Skill Familiar",
		style: {
      fontSize: "35px",
    },
  },
  // X軸設定
  xAxis: {
		// X軸 欄位名稱 設定
    categories: categories.value,
  },
  // Y軸設定
  yAxis: {
    title: {
      text: "",
    },
  },
	// 欄位顏色按照 colors 去分配顏色
  plotOptions: {
    column: {
      colorByPoint: true,
    },
  },
	// 數據顯示
  series: [
    {
      name: "Familiar 100% Upper Limit",
      data: seriesData.value,
    },
  ],
};
```

