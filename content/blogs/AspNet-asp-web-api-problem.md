---
title: ASP.NET WEB API常見問題
date: 2022-07-19 13:47:37
categories: Asp.net
---


#### <font color='red'>1. ASP.NET Core 中強制執行 HTTPS</font>

**說明：**
- **測試的時候可能會出現的問題 http導到https**
- **要求所有要求都需要 HTTPS。**
- **將所有 HTTP 要求都重新導向至 HTTPS。**

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddRazorPages();

var app = builder.Build();

if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();　／／　這個方法　會強制導到　https (建立專案測試時 請先不要用)

app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapRazorPages();

app.Run();
```