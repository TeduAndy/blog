---
title: C# 將資料輸出成 excel 方法
date: 2022-07-21 09:35:18
categories: C-sharp
---


## 使用到的套件
```C#
using Excel = Microsoft.Office.Interop.Excel;
```

<br>

## 操作方法

#### **<font color='red'>1. 設定需要用到變數</font>**
```C#
// 設定需要用到的變數

Excel.Application excelApp; // execl 使用的應用程式 變數  
Excel._Workbook wBook;	// 活頁簿 變數
Excel._Worksheet wSheet1; // sheet 變數1
Excel._Worksheet wSheet2; // sheet 變數2
Excel.Range wRange; // 活頁簿欄位範圍裏面的控制 及 操作 變數
```

#### **<font color='red'>2. 創建新的 excel 應用</font>**
```C#
// 開啟一個新的應用程式
excelApp = new Excel.Application();

// 讓Excel文件可見
excelApp.Visible = false;

// 停用警告訊息
excelApp.DisplayAlerts = false;

// 加入新的活頁簿
excelApp.Workbooks.Add(Type.Missing);

// 引用第一個活頁簿
wBook = excelApp.Workbooks[1];

// 基本創建第一個活頁簿時 就有一個 sheet工作表 這邊是添加第二個
wBook.Sheets.Add();

// 設定活頁簿焦點
wBook.Activate();

```

#### **<font color='red'>3. 針對當前活頁簿 操作應用</font>**
```C#
// 設定兩個工作表
wSheet1 = (Excel._Worksheet)wBook.Worksheets[1];
wSheet2 = (Excel._Worksheet)wBook.Worksheets[2];

// 設定兩個工作表的名稱
wSheet1.Name = "資料齊全";
wSheet2.Name = "資料不齊全";

// 設定工作表1為控制焦點，控制工作表2 也是 同樣方法
wSheet1.Activate();

// 對應 x y 座標 欄位 填入資料 方法
excelApp.Cells[1, 1] = "AA";

// 需要控制的欄位範圍 從 (x:1, Y:1) 到 (x:30, Y:32) 區塊的控制
wRange = wSheet1.Range[wSheet1.Cells[1, 1], wSheet1.Cells[30, 32]];

// 文字居中
wRange.HorizontalAlignment = Excel.XlHAlign.xlHAlignCenter;

// 文字加粗
wRange.Font.Bold = true;

// 選取 rang 全部
wRange.Select();

// 欄位自動調整
wRange.Columns.AutoFit();

```

#### **<font color='red'>4. 輸出 excel 並且指定到設定的位置</font>**
```C#
// 設定儲存檔名，不用設定副檔名，系統自動判斷 excel 版本，產生 .xls 或 .xlsx 副檔名
string pathFile = "";

//另存活頁簿
wBook.SaveAs(pathFile, Type.Missing, Type.Missing, Type.Missing, Type.Missing, Type.Missing, Excel.XlSaveAsAccessMode.xlNoChange, Type.Missing, Type.Missing, Type.Missing, Type.Missing, Type.Missing);

//關閉活頁簿
wBook.Close(false, Type.Missing, Type.Missing);

//關閉Excel
excelApp.Quit();

//釋放Excel資源
System.Runtime.InteropServices.Marshal.ReleaseComObject(excelApp);
wBook = null;
wSheet1 = null;
wSheet2 = null;
wRange = null;
excelApp = null;
GC.Collect();
```