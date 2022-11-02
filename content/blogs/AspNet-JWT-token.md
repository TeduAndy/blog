---
title: JWT 驗證 及 創建 token
date: 2022-07-19 11:00:35
categories: Asp.net
---

##### 使用的套件: <font color='red'>Microsoft.AspNetCore.Authentication.JwtBearer</font>

<br>

### <font color='red'>創建TOKEN</font>

+  **1. 先在 專案裡面 添加一個 JWT類 代碼如下：**

```C#
using System;
using System.Collections.Generic;
using System.Security.Claims;
using System.Text;
using System.IdentityModel.Tokens.Jwt;
using Microsoft.Extensions.Configuration;
using Microsoft.IdentityModel.Tokens;

namespace test2
{
    public class JWT
    {
        private readonly IConfiguration Configuration;

        public JWT(IConfiguration configuration)
        {
            this.Configuration = configuration;
        }

        public string GenerateToken(string userName, int expireMinutes = 30)
        {
            // 獲取在 appsettiongs.json 裡面設定好的資訊
            var issuer = Configuration.GetValue<string>("Jwt:Issuer");
            var signKey = Configuration.GetValue<string>("KEY:skey");

            // Configuring "Claims" to your JWT Token
            var claims = new List<Claim>();

            // In RFC 7519 (Section#4), there are defined 7 built-in Claims, but we mostly use 2 of them.
            //claims.Add(new Claim(JwtRegisteredClaimNames.Iss, issuer));
            claims.Add(new Claim(JwtRegisteredClaimNames.Sub, userName)); // User.Identity.Name
            //claims.Add(new Claim(JwtRegisteredClaimNames.Aud, "The Audience"));
            claims.Add(new Claim(JwtRegisteredClaimNames.Exp, DateTimeOffset.UtcNow.AddMinutes(20).ToUnixTimeSeconds().ToString()));
            //claims.Add(new Claim(JwtRegisteredClaimNames.Nbf, DateTimeOffset.UtcNow.ToUnixTimeSeconds().ToString())); // 必須為數字
            //claims.Add(new Claim(JwtRegisteredClaimNames.Iat, DateTimeOffset.UtcNow.ToUnixTimeSeconds().ToString())); // 必須為數字
            claims.Add(new Claim(JwtRegisteredClaimNames.Jti, Guid.NewGuid().ToString())); // JWT ID

            // The "NameId" claim is usually unnecessary.
            //claims.Add(new Claim(JwtRegisteredClaimNames.NameId, userName));

            // This Claim can be replaced by JwtRegisteredClaimNames.Sub, so it's redundant.
            //claims.Add(new Claim(ClaimTypes.Name, userName));

            // TODO: You can define your "roles" to your Claims.
            // claims.Add(new Claim("roles", "Admin"));
            //claims.Add(new Claim("roles", "Users"));

            var userClaimsIdentity = new ClaimsIdentity(claims);

            // Create a SymmetricSecurityKey for JWT Token signatures
            var securityKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(signKey));

            // HmacSha256 MUST be larger than 128 bits, so the key can't be too short. At least 16 and more characters.
            // https://stackoverflow.com/questions/47279947/idx10603-the-algorithm-hs256-requires-the-securitykey-keysize-to-be-greater
            var signingCredentials = new SigningCredentials(securityKey, SecurityAlgorithms.HmacSha256Signature);

            // Create SecurityTokenDescriptor
            var tokenDescriptor = new SecurityTokenDescriptor
            {
                Issuer = issuer,
                //Audience = issuer, // Sometimes you don't have to define Audience.
                //NotBefore = DateTime.Now, // Default is DateTime.Now
                //IssuedAt = DateTime.Now, // Default is DateTime.Now
                Subject = userClaimsIdentity,
                //Expires = DateTime.Now.AddMinutes(expireMinutes),
                SigningCredentials = signingCredentials
            };

            // Generate a JWT securityToken, than get the serialized Token result (string)
            var tokenHandler = new JwtSecurityTokenHandler();
            var securityToken = tokenHandler.CreateToken(tokenDescriptor);
            var serializeToken = tokenHandler.WriteToken(securityToken);

            return serializeToken;
        }
    }
}
```

<br>

+  **2. 接下來是到 Program.cs 註冊JWT類 需放在 var app = builder.Build(); 之前  代碼如下：**

```C#
builder.Services.AddSingleton<JWT>();
```

<br>

+  **3. 在 appsettings.json 設定 自己的私鑰 例：**

```json
"KEY": {
    "skey": "1234567890123456"
},
"Jwt": {
    "Issuer": "test2Demo"
}
```

<br>

+  **4. 接下來 在 controller 裡面 創建 JWT類 的空變量, 並且在建構函數設定 啟動 controller 時候注入 並且賦值到 創建好的JWT空變量**

```C#
public class UserController : Controller
{
    private readonly JWT jwt;
    public UserController(JWT _jwt)
    {
        jwt=_jwt;
    }
}		
```

<br>

### <font color='red'>驗證TOKEN</font>

+  **1. 請求上面 加入這段 [Authorize] 便會判斷 請求是需要 TOKEN 驗證的, [AllowAnonymous] 則允許未經驗證的使用者存取個別動作**

```C#
// 需要驗證
[Authorize]
[HttpGet]
public ActionResult<User> Index()
{
}

// 不需要驗證
[AllowAnonymous]
[HttpGet]
public ActionResult<User> Index()
{
}	
```

<br>

+  **2. 接下來在 var app = builder.Build() 之前 加入這段驗證確認設定;**

```C#
builder.Services
    // .AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddAuthentication(options =>{
                // 設定使用者預設的 Authenticate、authentication challenge 的 Scheme 都設定為 JwtBearerDefaults.AuthenticationScheme
                options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
                options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
                })
    .AddJwtBearer(options =>  {
        // 當驗證失敗時，回應標頭會包含 WWW-Authenticate 標頭，這裡會顯示失敗的詳細錯誤原因
        options.IncludeErrorDetails = true;

        options.TokenValidationParameters = new TokenValidationParameters
        {
            // 透過這項宣告，就可以從 "sub" 取值並設定給 User.Identity.Name
            NameClaimType = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier",
            // 透過這項宣告，就可以從 "roles" 取值，並可讓 [Authorize] 判斷角色
            RoleClaimType = "http://schemas.microsoft.com/ws/2008/06/identity/claims/role",

            // 一般我們都會驗證 Issuer
            ValidateIssuer = true,
            ValidIssuer = builder.Configuration.GetValue<string>("Jwt:Issuer"),

            // 通常不太需要驗證 Audience
            ValidateAudience = false,
            //ValidAudience = "JwtAuthDemo", // 不驗證就不需要填寫

            // 一般我們都會驗證 Token 的有效期間
            ValidateLifetime = true,

            // 如果 Token 中包含 key 才需要驗證，一般都只有簽章而已
            ValidateIssuerSigningKey = false,

            // "1234567890123456" 應該從 IConfiguration 取得
            IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(builder.Configuration.GetValue<string>("KEY:skey")))
        };
    });
```

<br>

+  **3. 再之後在 app.UseHttpsRedirection(); 後面 加入這兩行**

```C#
// 驗證中間件，以服務容器註冊的驗證服務檢查是否有驗證
app.UseAuthentication();
// 授權中間件，從驗證資訊、路由對應、授權設定判斷是否能夠存取所要求的資源
app.UseAuthorization();
```


