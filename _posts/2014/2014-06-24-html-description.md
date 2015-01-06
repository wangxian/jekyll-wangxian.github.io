---
layout: post
comments: true
title: "html meta description"
category: ""
tags: 
  - 开发
---

突然发现一个问题，前几天把网站 _layout/default.html 中的添加了`HTML>META[description]`属性，
这导致了一个比较严重的问题，Google收录网站，Google搜出来的所有描述，
都变成了设置成的description信息。

查了一下`HTML>META[description]`的使用场景。

    description用于定义网页简短描述
    description出现在name属性中，使用content属性提供网页的简短描述

不能每个页面的描述信息都一样，尤其是文章页。最后加上了判断，只有首页有完整的描述信息。
别的界面没有描述信息。

\- 完 - 