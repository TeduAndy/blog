---
title: Dapper 使用介紹
date: 2022-07-19 09:27:01
categories: Asp.net
---


## **<font color='red'>說明：</font>**

- **Dapper輕量級的 ORM，必須要自己定義 C# class、管理連線、自己寫 SQL，但是套件非常迷你而且效能非常好，很適合已經學會目標資料庫語法的開發者。**

<br>

### **<font color='red'>安裝：</font>**

**1. 專案點右鍵 -> 管理 NuGet 套件**

**2.** **收尋 1. [Dapper](https://www.nuget.org/packages/Dapper) and 1. [MySQL Connector](https://www.nuget.org/packages/MySqlConnector/) 並且安裝**

<br>

##  **<font color='red'>Dapper 連線 :</font>** 

+ **1. 定義一個用來接資料的 Model 類別：**
	**Dapper 支援泛型，只要把指定的型別告訴 Dapper，而且類別的屬性與 MySQL 的欄位有對上，Dapper 就會自動幫我們把取回來的資料放進 Model 類別。**

<br>

+ **2.開啟一個 MySQL 連線：**
	**用 `var _db = new MySqlConnection("連線資訊");`
	就能開啟連線。比較需要注意的是，最好用注入組態設定的方法取得連線資訊，以及用 using 語法自動幫我們關閉連線，以免忘記關閉造成連線被占用**

<br>

+ **3.連線資訊設定：**
   **在專案新增一個空類 名叫 serverMq.cs 裡面是用來填入 我們從組態設定抓來的 連線字串**
```C#
public class servermq
{
	public string ConnectionString { get; set; }
}
```
<center style="font-weight:600"> 到 appsettings.json 組態設定裡面 新增 mysql 連線字串</center>

```json
"AllowedHosts": "*",
"MySQL": {
	"ConnectionString": "server=127.0.0.1;userid=用戶名字;password=密碼;database=連線的資料庫名字;"
}
```
<center style="font-weight:600"> 然後在 Program.cs 裡面設定 啟動時 抓取 連線字串 並且 注入到 我設定好的容器</center>

```C#
builder.Services.Configure<servermq>(builder.Configuration.GetSection("MySQL"));
```
<center style="font-weight:600"> 然後在 controller 裡面的 controller建構函數 啟動時 把 注入的 servermq 注入到 設定好的空 _options</center>

```C#
private readonly servermq _options;

public UserController(IOptions<servermq> options)
{
	_options = options.Value;
}

// 取 連線字串
var _db = new MySqlConnection(_options.ConnectionString);

// 便可以連接到 mysql 
```

<br>

##  **<font color='red'>Dapper使用: </font>** 

<br>

## **<font color='orange'> 1. Dapper - Query </font>** 
**光是查詢Dapper就提供了很多種方法可以使用，很多方法都跟Lambda用法一樣。**

- [**Query**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#Query)
- [**QueryFirst**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#QueryFirst)
- [**QueryFirstOrDefault**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#QueryFirstOrDefault)
- [**QuerySingle**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#QuerySingle)
- [**QuerySingleOrDefault**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#QuerySingleOrDefault)
- [**QueryMultiple**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#QueryMultiple)

```C#
List<MyModel> results = null;
using (SqlConnection conn = new SqlConnection(strConnection))
{
	string strSql ="Select * from Users" ;
	results = conn.Query<MyModel>(strSql).ToList();
}
```

<br>

##### **<font color='orange'> 2. Dapper - Execute </font>** 

**執行Insert、Update、Delete、Stored Procedure時使用。**

- [**Stored Procedure**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#Stored%20Procedure)
- [**INSERT statement**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#INSERT%20statement)
- [**UPDATE statement**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#UPDATE%20statement)
- [**DELETE statement**](https://dotblogs.com.tw/OldNick/2018/01/15/Dapper#DELETE%20statement)

**新增多筆範例 (修改\刪除也是同一種方法, 只是 sql 不同)**

```C#
//新增多筆範例
using (SqlConnection conn = new SqlConnection(strConnection))
{
	string strSql ="INSERT INTO Users(col1,col2) VALUES (@c1,@c2);" ;
	//新增多筆參數
	dynamic datas = new []{ new { c1 = "A", c2 = "A2" }
				, new { c1 = "B", c2 = "B2" }
				, new { c1 = "C", c2 = "C2" }};
	conn.Execute( strSql, datas);
}
```

<br>

##### **<font color='orange'> 3. Dapper - Async </font>** 

**非同步方法Dapper也是有提供，寫法只有一點點不一樣而已。**

- **ExecuteAsync**
- **QueryAsync**
- **QueryFirstAsync**
- **QueryFirstOrDefaultAsync**
- **QuerySingleAsync**
- **QuerySingleOrDefaultAsync**
- **QueryMultipleAsync**

**寫法沒多大改變，除了方法名稱不一樣以外，最大的不同是要.Result**

```C#
List<MyModel> results = null;
using (SqlConnection conn = new SqlConnection(strConnection))
{
	string strSql ="Select * from Users" ;
	//非同步
	results = conn. QueryAsync<MyModel>(strSql).Result.ToList();
}
```


