---
title: C# mysql_conn
date: 2022-07-18 15:49:56
categories: C-sharp
---

### 一.  引入 需要的套件

```C#
using MySql.Data.MySqlClient;
```

<br>

### 二.  先有連線字串

```C#
string connString = "server=127.0.0.1;port=3306;user id=root;password=***;database=mvctest;charset=utf8;";
```

<br>

### 三.  建立一個Connection(聯繫), 連線跟字串連結起來

```C#
MySqlConnection conn = new MySqlConnection();
conn.ConnectionString = connString;
```

<br>

### 四.  連線打開，如果已經開了，再打開一次會出錯，要先判斷

```C#
if (conn.State != ConnectionState.Open)
{
	conn.Open();
}
```

<br>

### 五.  創建 Command(命令) 並且執行 然後判斷成功與否

```C#
// sql 字符串 
	string sql = @"INSERT INTO MTN100 (AREA, CARDNUMBER, SAMFILE) VALUES ("SA", "0936050029001000000266", file)
// 創建命令 
	MySqlCommand cmd = new MySqlCommand(sql(sql串), conn(聯繫)); 
// 執行 
	int index = cmd.ExecuteNonQuery(); 
// 判斷成功與否
	bool success = false;
// 判斷 傳回的 index 是否大於 0
	if (index > 0)
	{
		success = true;
	}
	else
	{
		success = false;
	}
```

#### <span style="color:red">ExecuteNonQuery</span> 方法 用在新增修改刪除, 成功返回受影響的列數, 失敗傳回0

<br>

### 六.  使用完也要關閉

```C#
conn.close();
```