---
title: Custom Authorization TagHelper for Aspnet Core
author: tmacharia
date: '2021-09-24 21:53:16'
layout: post
comments: true
tags:
- aspnet-core
- authorization
- razor
image: assets/auth-tag-helpers-blog-banner.jpg
---

![]({{ 'assets/auth-tag-helpers-blog-banner.jpg' | relative_url }})
Tag helpers enable server-side code to participate in creating and rendering HTML elements in Razor files.

**What Tag Helpers provide**
* An HTML-friendly development experience.
* A rich IntelliSense environment for creating HTML and Razor markup.
* A way to make you more productive and able to produce more robust, reliable, and maintainable code using information only available on the server.

[Read more about Tag Helpers in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-5.0)

#### Render HTML elements based on User Role
Normally, if you want to hide/show  HTML elements based on a user's role, you would have to write something like this to make it happen.
```html
@if(User.IsInRole("Admin"))
{
    <button role="button">Approve</button>
}
```

... to be continued (felt tired 🚶🏻‍♂️)
