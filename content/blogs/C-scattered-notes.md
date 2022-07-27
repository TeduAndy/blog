---
title: C# 散亂筆記
date: 2022-07-18 16:44:47
categories: C-sharp
---

<span style="color:red; font-size:25px; font-weight:600">
	Process 呼叫EXE 檔案 並 傳值 
</span>

```C#
// 第二個負責傳參數 用 空格 分別不同 值

Process.Start("C:\\AP06BZ\\EXE\\MTNP200.exe", "2407 L123370532");

```

<br>

<span style="color:red; font-size:25px; font-weight:600">
	匿名函數說明
</span>

```C#
() => expression  // expression = 求值式 本身會有  return value
() => { statement; } // statement  = 執行語句，需要 return 才會 return
```
