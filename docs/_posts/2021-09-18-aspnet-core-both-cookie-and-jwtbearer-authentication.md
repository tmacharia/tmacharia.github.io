---
title: Aspnet Core Both Cookie And JwtBearer Authentication
date: '2021-09-18 07:25:21'
layout: post
tags:
- aspnet-core
- jwt
- cookies
- authentication
- authorization
author: tmacharia
categories:
- coding
---

Easy step-by-step procedure for enabling and using both Cookie & JwtBearer Authentication in AspnetCore web project. The main objective is to have our APIs authenticate & authorize requests with either a valid Bearer AccessToken coming from Mobile Apps for example, or Cookies coming from Ajax requests.

#### 1. Add Authentication Service
And configure default authentication options as follows.
```cs
services.AddAuthentication(options =>
{
    options.DefaultSignInScheme = CookieAuthenticationDefaults.AuthenticationScheme;
    options.DefaultAuthenticateScheme = CookieAuthenticationDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = CookieAuthenticationDefaults.AuthenticationScheme;
    options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
})
```
#### 2. Add Cookie
Add cookie authentication using the default scheme & additional options. It's important to use a custom cookie name, we'll see why later.
```cs
.AddCookie(CookieAuthenticationDefaults.AuthenticationScheme, x =>
{
    x.Cookie.Name = "MyCookie";
})
```
#### 3.  Add Jwt Bearer
Add JWT Bearer authentication & specify token generation & validation options/requirements.
```cs
.AddJwtBearer(x =>
{
    x.SaveToken = true;
    x.RequireHttpsMetadata = false;
    x.TokenValidationParameters = new TokenValidationParameters()
    {
        ValidateIssuer = true,
        ValidateAudience = true,
        ValidateLifetime = true,
        ValidIssuer = identityConfig.Issuer,
        ValidAudience = identityConfig.Audience,
        ValidateIssuerSigningKey = true,
        ClockSkew = TimeSpan.FromMinutes(1),
        IssuerSigningKey = new SymmetricSecurityKey(Encoding.ASCII.GetBytes(identityConfig.Secret))
    };
})
```
`identityConfig` in this case is a class instance used to read config/sensitive information in `appsettings.json`.
#### 4. Add Custom Policy Scheme
Add an additional custom policy scheme called `Mixed` and specify rules for determining which authentication scheme to use at runtime. 
Define rules that best suit your use case, some examples:
* Check Request for Authorization Bearer Header.
* Check Request Path
* Check Request Cookies.

```cs
.AddPolicyScheme("Mixed", "Cookie/JwtBearer", x =>
{
    x.ForwardDefaultSelector = context =>
    {
        bool isApi = context.Request.Path.StartsWithSegments("/api", StringComparison.InvariantCulture);
        if (isApi == false)
            return CookieAuthenticationDefaults.AuthenticationScheme;
        else
        {
            bool hasAuthCookie = context.Request.Cookies.ContainsKey("MyCookie");
            if (hasAuthCookie)
                return CookieAuthenticationDefaults.AuthenticationScheme;
            else
            {
                return JwtBearerDefaults.AuthenticationScheme;
            }
        }
    };
    x.ForwardForbid = JwtBearerDefaults.AuthenticationScheme;
});
```

And that's basically it. Just kidding, time to apply.

#### 5. Default MVC Views
Since cookie authentication is the default, using `[Authorize]` as usual in controller actions for views, will work just fine.
#### 6. Mixed API Routes
For API routes that you want to leverage either Cookie or Bearer Auth, add `[Authorize]`attribute but specify the scheme as follows.
```cs
[Authorize(AuthenticationSchemes = "Mixed")]
```

### References
* [https://stackoverflow.com/questions/49455943/asp-net-core-webapi-cookie-jwt-authentication](https://stackoverflow.com/questions/49455943/asp-net-core-webapi-cookie-jwt-authentication)
* [https://stackoverflow.com/questions/46938248/asp-net-core-2-0-combining-cookies-and-bearer-authorization-for-the-same-endpoin](https://stackoverflow.com/questions/46938248/asp-net-core-2-0-combining-cookies-and-bearer-authorization-for-the-same-endpoin)
