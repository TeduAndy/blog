---
title: C# HttpClient
date: 2022-12-12 16:00:22
categories: C-sharp
---

### **說明：**
- **HttpClient 提供許多非同步方法獲取 HTTP 內容，有 GET / POST / PUT / DELETE...等等**
- **HttpClient 是用於從 URI 標示的資源發送 HTTP 請求和接收 HTTP 響應的基類**

<br>

### **非同步方法：**
- DeleteAsync
- GetAsync
- GetByteArrayAsync
- GetStreamAsync
- GetStringAsync
- PostAsync
- PutAsync
- SendAsync

<br>

### **POST 和 GET 非同步教學：**

<br>

##### GET
```C#

using (HttpClient client = new HttpClient())
{
	// 執行 GET非同步方法
	HttpResponseMessage res = await client.GetAsync(url);

	// 用於拋出異常
	res.EnsureSuccessStatusCode();
	
	// T 要返回哪類型別
	result = await res.Content.ReadAsAsync<T>();
}

```

<br>

##### POST
```C#
public class infoDTO
{
	public string name {get;set;}
	public string phone {get;set;}
}


using (HttpClient client = new HttpClient())
{
	string result = "";
	string url = "https://127.0.0.1:443/post";
	using(HttpClient client = new HttpClient())
	{
		// 創建 data 物件
		infoDTO obj = new infoDTO();
		obj.name = "Andy"
		obj.phone = "00-00000000"

		// 將物件轉成 json string
		string jsonStr = JsonConvert.SerializeObject(obj);
		HttpContent data = new StringContent(jsonStr);

		// 設置傳輸格式
		data.Headers.ContentType = new MediaTypeHeaderValue("application/json");

		// 執行 post 非同步請求
		HttpResponseMessage res =  await client.PostAsync(url, data);

		// 拋錯使用
		res.EnsureSuccessStatusCode();

		// 成功之後將響應回來的資訊讀取出來
		result = await res.Content.ReadAsStringAsync();
	}
}
```


