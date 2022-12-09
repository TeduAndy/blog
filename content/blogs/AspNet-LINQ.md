---
title: LINQ 相關
date: 2022-07-19 10:00:01
categories: Asp.net
---

#### **<font color='red'>Datatable 用法</font>**

```C#
// 抓回來的 DataTable
DataTable tb = GetTB(_formno, _key);

// tb.AsEnumerable() 會轉成 EnumerableRowCollection<DataRow> 類型 , 因為是 Enumerable 類型 便可以用 linq 


// 從裡面的資料抓取多筆 使用 where , {} 內是要寫第二行 但是 {} 不會自動 return 所以要手動 return
var tmps = tb.AsEnumerable().Where(row =>
            {
                var num = row["DTLNO"].ToString();
                return (Convert.ToInt32(num) < 220 && num != "215") | num == "254";
            });


// 單一一筆 使用 FirstOrDefault (但是這個會 一抓到一筆 馬上返回)
var tmp = tb.AsEnumerable().FirstOrDefault(row => row["DTLNO"].ToString() == "215");


// 單一一筆 使用 SingleOrDefault (這個是抓到一筆 會再繼續往下 查完所有 抓到第二筆則會報錯誤)
tmp = tb.AsEnumerable().SingleOrDefault(row => row["DTLNO"].ToString() == "252");
```


