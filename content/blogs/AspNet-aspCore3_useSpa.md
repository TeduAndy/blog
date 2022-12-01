---
title: ASP.NET CORE 3.1 將靜態資源資料夾放入 VUE
date: 2022-11-30 13:47:37
categories: Asp.net
---


### **說明：**
- 撰寫前後端分離的專案，通常都是分別各起一個應用程式。
- 也可以將後端讀取靜態資源的資料夾，當成前端的起始點。

<br>

### **設置教學**
- 使用套件：Microsoft.AspNetCore.SpaServices.Extensions (目前使用版本：3.1.25)
- 通常靜態資源都會放入一個 wwwRoot 的資料夾，如果沒有的話可以創建一個 wwwRoot 資料夾
- 接下來則是在 Startp.cs 裡面進行配置

<br>

#### 註釋的地方是要添加進去的地方
```C#
 public class Startup
    {
        public Startup(IConfiguration configuration)
        {
            Configuration = configuration;
        }

        public IConfiguration Configuration { get; }

        public void ConfigureServices(IServiceCollection services)
        {
            services.AddControllers();
        }

        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseHttpsRedirection(); 

			// 沒有指定檔案名稱的話就預設使用 index.html  http://xxx.xxx.xx/controller/(index.html)
            app.UseDefaultFiles(); 
			
			// 預設把  wwwRoot 資料夾底下的檔案作為靜態資源提供服務
            app.UseStaticFiles(); 

            app.UseRouting();

            app.UseAuthorization();

            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllers();
            });
            // 404 not found
            // 把後端收到的 http://xxx.xxx.xx/app/.... 請求 全部導到 http://xxx.xxx.xx/app/index.html 並告訴前端 /a/b/c
			// 這段是有安裝套件才能使用！
            app.UseSpa(spa => {
                spa.Options.SourcePath = "/app";
            });
        }
    }
```