---
title: 使用 Serilog 對應用程式事件進行結構化紀錄
date: 2022-07-19 13:39:29
categories: Asp.net
---

### **版本:Asp.net 6**

<br>

### 1. <font color='#9f6b53'>使用的套件:</font>
+ **Serilog 版本: 2.11.1**
+ **Serilog-AspNetCore 版本: 6.00**

<br>

### 2. <font color='#9f6b53'>Asp.net6  Program.cs 設定:</font>

```C#
using System;
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Serilog;
using Serilog.Events;

    // LOG基本設定
    Log.Logger = new LoggerConfiguration()
        .MinimumLevel.Information()
        .MinimumLevel.Override("Microsoft.AspNetCore", LogEventLevel.Warning)
        .WriteTo.Console() // 執行 LOG時 輸出也會打印
        .WriteTo.File("../logs/log-.txt", rollingInterval: RollingInterval.Day) // 輸出到哪一個資料夾
        .CreateLogger();
  
    try
    {
        Log.Information("=============Starting=============");

        // TODO: 將原本 Program.cs 所有程式碼搬到這裡

        // LOG設定 必須在 APP 之前
        builder.Host.UseSerilog();

        // app.UseSerilogRequestLogging(); 這個 Middleware 來整理所有與 Request 相關的紀錄，讓你在一條 Log 中就可以取得目前 Request 所有的相關資訊。
        app.UseSerilogRequestLogging();
        
        return 0;
    }
    catch (Exception ex)
    {
				 // web 運作錯誤 寫入
        Log.Fatal(ex.Message);
        return 1;
    }
    finally
    {
				// 結束時 關閉
        Log.CloseAndFlush();
    }
```

<br>

### 3. <font color='#9f6b53'>Asp.net6  Controller 使用:</font>

```C#
// ILogger<當前controller>
private readonly ILogger<Controller> _logger;

public 建構函數(ILogger<Controller> logger)
{
	_logger = logger;
}
```

<br>

### 4. <font color='#9f6b53'>Log 注入訊息有哪些方法:</font>

```C#
// Log 可以使用的方法 用來判別 錯誤訊息 還是正確訊息
logger.Verbose("Hello");
logger.Debug("Hello");
logger.Information("Hello");
Log.Warning("Hello");
logger.Error("Hello");
logger.Fatal("Hello");
```