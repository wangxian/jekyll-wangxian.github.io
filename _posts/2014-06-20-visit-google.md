---
layout: post
comments: true
title: "访问谷歌"
category: ""
tags: 
  - Google
---

访问Google成了一个技术活了。

试法多种，唯`SSH`隧道法最简单，具体步骤不多说，自己搜索。

使用软件：Firefox(如果是Chrome需装插件) + SSH

~~~
ssh -D 8822 -f -C -q -N root@domain.com
~~~
