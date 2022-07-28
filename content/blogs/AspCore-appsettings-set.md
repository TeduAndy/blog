---
title: 組態設定 appsettings.json
date: 2022-07-19 10:51:27
categories: Asp.net core 
---


### **<font color='red'>說明：</font>**
**在 appsettings.json 自己所需要的參數 避免在邏輯控制層曝露自己的帳號密碼, 只有在邏輯控制啟動時注入 到 自己寫好的 DTO裡面 並且實例化**

<br>

### **<font color='red'>使用方法：</font>**

+  **1. 先在 appsettings.json 設定自己需要的 參數 例: 設定了一個 mysql 裡面的 connectionstring**

```json
"AllowedHosts": "*",
  "MySQL": {
      "ConnectionString": "server=127.0.0.1;userid=root;password=123456;database=django;"
  },
```

<br>

+  **2. 然後先寫好自己要注入的DTO**

```C#
namespace test2
{
	public class servermq
	{
		public string? ConnectionString { get; set; }
	}
}
```

<br>

+  **3. 然後在 Program.cs 裡面添加 這段 (基本上 appsettings.json 獲取裡面的資訊都是用這方式)**

```C#
builder.Services.Configure<servermq>(builder.Configuration.GetSection("MySQL"));
```

<br>

+  **4. 然後在 Controller 那裡 先幫 創好 一個變量 , 然後在他的建構函數下 添加這段.**

```C#
[ApiController]
[Route("[Controller]")]
public class UserController : Controller
{
	private readonly servermq _options;

	//建構函數
	public UserController(IOptions<servermq> options)
	{
		// 啟動時注入 並且把 值 賦予到 創好的變量裡面 
		_options = options.Value;
	}
}
```