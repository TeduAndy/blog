---
title: C# PrintDocument 元件列印說明 (winform)
date: 2022-07-18 16:37:54
categories: C-sharp
---

### **<span style="color:red"> 說明： </span>**
	一般來說 用 winform 寫 列印 相當麻煩 因為要對應 位置 以及 以及會使用到多個元件 對此 針對這個部分來做一些說明

<br>

### **<span style="color:red"> 使用方法： </span>**

#### 1.先在 需要 綁定的按鈕 創建點擊事件，並且在事件裡面 產生一個 PrintDocument 物件 如圖

```C#
private void button1_Click(object sender, EventArgs e)
{
	// 創建列印物件 
	PrintDocument pd = new PrintDocument();
	// 並且 加入 啟動列印時 該執行的動作(method)， but 這個方法傳遞參數那邊 必須設置 object sender, PrintPageEventArgs ev 這兩個
	pd.PrintPage += new PrintPageEventHandler(this.pd_PrintPage);
	// 啟動列印
	pd.Print();

	// 但是在 真正列印的時候 會先預覽 去看 文字或者文字的位置以及大小，才會去做真正的列印，這時候可以先把 print() 先註釋 先使用預覽模式 把 PrintDocument 綁定到 PrintPreviewDialog
	PrintPreviewDialog pD = new PrintPreviewDialog();
	pD.Document = pd;
	pD.ShowDialog();
}
```

<br>

#### 2.接下來需要在 該執行的動作(method) 裡面 設置 我們要的文字及圖片

```C#
//記得傳值參數須帶上 object sender, PrintPageEventArgs ev 
private void pd_PrintPage(object sender, PrintPageEventArgs ev)
{
	// 文字大小以及是甚麼文字體
	var printFont = new Font("Arial", 10);
	// 字體顏色
	var color_font = Brushes.Black;
	// 座標
	var coordinate = new PointF(300, 300)
	// 寫入文字的方法
	ev.Graphics.DrawString("要輸出的內容", printFont, color_font, coordinate );


	// 獲取圖片
	Image newImage = Image.FromFile("圖片地址");
	// 繪製圖片擺放位置以及大小控制 
	Rectangle destRect = new Rectangle(100, 100, 200, 100); // (前兩個是座標位置，後面兩個是設定大小)
	// 圖片 寫入的方法	
	ev.Graphics.DrawImage(newImage, destRect);
}
```