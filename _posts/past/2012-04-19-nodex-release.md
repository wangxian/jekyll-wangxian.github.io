---
layout: post
title: NodeX 预览版 发布了！
category: Node.js
tags: ['JavaScript', 'Node.js', 'NodeX']
---

经过不断的折腾，终于nodex 预览版发布了，

## nodex 是什么？

nodex 是一个基于node.js的web framework，用它你可以快速构建一个web项目，相比较与PHP，你可以有更多的权限，
控制服务器为你服务，比如，全局变量，内存缓存(global一个变量即可) 等；

node.js对处理高并发，相比PHP，会更的心应手，效率更高。
nodex 是一个基于 node.js 的webserver(服务器和程序一体)，nodex和我的另一个开源项目 <a href="https://github.com/wangxian/ePHP" target="_blank">ePHP</a> 规范基本一致。 url，constroller/action 。

node.js有一个比较有名的框架`express` , 那为什么还要开发一个呢？
因为express基于connect中间件，路由规则，非常的麻烦，nodex非常的简单、高效，你可以修改nodex.js的代码，快速构建一个web application.

nodex主要在node.js基础上添加了：控制器调度、session、cookie、模版引擎

你可能用的第三方模块：mysql formidable mongodb mongoskin underscore ....


## 使用npm安装：

{% highlight sh %}
npm install nodex
{% endhighlight %}

然后，从github clone 检出目录结构，直接在此基础上开发（包含了一个小的todo示例）。

    git clone git://github.com/wangxian/nodex.git


然后进入git检出的目录，执行`node server.js `

（当然,前提是你你已经安装了node.js）


详细使用说明：<a href="https://github.com/wangxian/nodex" style="color:blue">https://github.com/wangxian/nodex</a>


--------------------------------
**nodex** 为一个简单的web framework，只要稍微熟悉node.js的语法，你就可以轻松的修改nodex，
快速构建一个小项目。

更新时间：2012-4-22
