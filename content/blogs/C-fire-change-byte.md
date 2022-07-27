---
title: C# 上傳檔案轉成二進制
date: 2022-07-18 16:00:22
categories: C-sharp
---

## 一、上傳檔案轉成二進制

```C#
try
{
	StreamReader sr = new StreamReader(openFileDialog1.FileName);
	var bytes = default(byte[]);
	using (var memstream = new MemoryStream())
	{
		sr.BaseStream.CopyTo(memstream);
		bytes = memstream.ToArray();
		//SetText(sr.ReadToEnd());
	}
catch(SecurityException ex)
{
	MessageBox.Show($"Security error.\n\nError message: {ex.Message}\n\n" + $"Details:\n\n{ex.StackTrace}");}
}
```

<br>

#### 一. StreamReader sr = new StreamReader(位置路徑); <span style="color:red"> (這邊輸出只是可讀 string 拿不到 byts) </span>

#### 二. var bytes = default(byte[]); 設置空的 bytes

#### 三. var memstream = new MemoryStream() <span style="color:red"> (呼叫一個 空的 不可讀 但可以拿到 byte 檔的容器) </span>

#### 四. sr.BaseStream.CopyTo(memstream); <span style="color:red"> (把可讀的複製到空容器裡面) </span>

#### 五. bytes = memstream.ToArray(); (最後 賦值給空 bytes)

<br>

## 二、把資料寫回本地

```C#
var RowData = SamTb.Rows[0]["SAMFILE"];
var data = (Byte[])SamTb.Rows[0]["SAMFILE"];
var sw = new FileStream(HisPath + HisPathName + FileEX, FileMode.OpenOrCreate);
sw.Write(data, 0, data.Count());
sw.close();
```

**new FileStream( <span style="color:red"> 寫入的位置, FileMode.選項是開啟已有檔案或者其他... </span> );**

**sw.Write( <span style="color:red"> 寫入的資料, 偏移量, 資料的長度 </span> );**

<br>

<div style="color:red; 
			text-align:center; 
			font-size:25px; 
			font-weight:600"
> 
	開啟檔案寫入後千萬記得關閉!!!!  
</div>

