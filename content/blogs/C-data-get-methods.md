---
title: C# 資料庫獲取資料
date: 2022-07-18 16:26:39
categories: C-sharp
---


### 說明：
	方法有兩種，一種是 DataTable 一種是 DataReader，最簡單的就是用 DataTable 接資料

<br>

```C#
string connString = "server=127.0.0.1;port=3306;user id=root;password=Acuteboy1215;database=mvctest;charset=utf8;";
MySqlConnection conn = new MySqlConnection();
public ActionResult Index()
{
	// 聯繫裡面放入連線字串
	conn.ConnectionString = connString;
  	string sql = @" SELECT `id`, `city` FROM `city`";
	
	// 創建新的空的 DataTable 讓抓回來的資料存放 
  	DataTable dt = new DataTable();

	// 執行 sql 語句
  	MySqlDataAdapter adapter = new MySqlDataAdapter(sql, conn);

	// 將資料注入到 空的 database
  	adapter.Fill(dt);
}
```

<br>

#### 在這段程式我們沒有處理 <span style="color:red"> 連線 </span> 跟 <span style="color:red"> 斷線 </span>，<span style="color:red"> 因為 MySqlDataAdapter 會幫我們處理 </span>
