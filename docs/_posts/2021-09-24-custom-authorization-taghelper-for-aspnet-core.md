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
image: https://i.pinimg.com/736x/e0/d3/44/e0d34427aa341b881dc5dd292edc1bd1.jpg
---

![hero-image](https://d585tldpucybw.cloudfront.net/sfimages/default-source/blogs/2018/2018-03/taghelpers_870x220.png)

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
