---
title: VUE 基礎理論
date: 2022-07-21 14:40:49
categories: vue
---

### <font color='red'>1. Vue的双向数据绑定原理:</font>
   **Vue是采用数据劫持结合发布订阅模式，通过Object.defineProperty()来劫持各个属性的getter,setter,**
   **在数据变动时发布消息给订阅者，触发相应的回调函数，从而实现数据双向绑定。**

<br>

### <font color='red'>2. SPA 单页面的理解，它的优缺点分别是什么？</font>
   **SPA（ single-page application ）仅在 Web 页面初始化时加载相应的 HTML、JavaScript 和 CSS。**
   **一旦页面加载完成，**
   **SPA 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 HTML 内容的变换，UI 与用户的交互，避免页面的重新加载。**

<br>

+ #### **優點：**
	+ **用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染**
	+ **基于上面一点，SPA 相对对服务器压力小**
	+ **前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理**

+ #### **缺點：**
	+ **初次加载耗时多：为实现单页 Web 应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一加载，部分页面按需加载**
	+ **前进后退路由管理：由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理**
	+ **SEO 难度较大：由于所有的内容都在一个页面中动态替换显示，所以在 SEO 上其有着天然的弱势。**

<br>

### <font color='red'>3、v-show 与 v-if 有什么区别？</font>

+ #### **V-if**
   **是真正的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建；**
   **也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。**
+ #### **v-show**
   **就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 的 “display” 属性进行切换。**
   **所以，v-if 适用于在运行时很少改变条件，不需要频繁切换条件的场景；**
   **v-show 则适用于需要非常频繁切换条件的场景。**

<br>

### <font color='red'>4、谈谈你对 Vue 生命周期的理解？</font>

+  #### **<font color='e59911' >beforeCreate</font>**
	**组件实例被创建之初，组件的属性生效之前**
+  #### **<font color='e59911' >created</font>**
	**组件实例已经完全创建，属性也绑定，但真实 dom 还没有生成，$el 还不可用**
+  #### **<font color='e59911' >beforeMount</font>**
	**在挂载开始之前被调用：相关的 render 函数首次被调用**
+  #### **<font color='e59911' >mounted</font>**
	**el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子**
+  #### **<font color='e59911' >beforeUpdate</font>**
	**组件数据更新之前调用，发生在虚拟 DOM 打补丁之前**
+  #### **<font color='e59911' >update</font>**
	**组件数据更新之后**
+  #### **<font color='e59911' >activited</font>**
	**keep-alive 专属，组件被激活时调用**
+  #### **<font color='e59911' >deactivated</font>**
	**keep-alive 专属，组件被销毁时调用**
+  #### **<font color='e59911' >beforeDestory</font>**
	**组件销毁前调用**
+  #### **<font color='e59911' >destoryed</font>**
	**组件销毁前调用**

<br>

### <font color='red'>5、在什么阶段才能访问操作DOM？</font>

+ ##### **mounted 中就可以访问操作 DOM**