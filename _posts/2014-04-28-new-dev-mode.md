---
layout: post
comments: true
title: "app seo seed"
category: "weeklog"
tags: 
  - weeklog
  - 开发
  - SEO
---

![](http://ww4.sinaimg.cn/large/493b785agw1efxf9fo0bgj20m80a6wgw.jpg)

> 周末花时间把一个想法变成了代码

主要让前端和后端开发藕合性降低，让网站或APP开发变为和手机移动开发类似的模式，  
一般后端开发的人都不怎么熟悉前端交互开发，所以让专业的人做专业的事情，资源最优配置嘛  

如果前端交互和渲染从服务器端移动到客户端，虽然减轻了服务器端的压力，\\
但带来了一个比较严重的问题 —— SEO  \\
如何解决这个问题？现在的技术发展已经不是问题了

解决的办法主要有：

1. 服务器提供特殊模板来渲染给搜索引擎蜘蛛
2. Google `#!` URL的解决办法
3. 服务器渲染启动浏览器实例，渲染前端界面抛给搜索引擎

第一种方法，提供特殊的模板，增加了工作量。第二种方法，google only\\
所以我采用了第三种办法，来做一个尝试。 做了一个seed，源码见 `github.com/wangxian/seo-express-seed` \\
后端服务器使用express, 使用phantomjs来渲染前端界面(好像还有一个webloop，也可以做同样的事情)\\

主要思路是，后端SERVER URL 路由，如果是 / 判断是不是Spider, 启动phantomjs来渲染，  
如果不是则正常 Server一个 static HTML给浏览器，其他的所有URL,
判断判断Spider\\
是：启动phantomjs来渲染\\
否: 301到前端去渲染(http://hostname/#!/article/2)

*测试*

    使用Chrome打开: 
    view-source:http://hk.wangxian.me/
    
    使用curl命令: 
    curl -A "Mozilla/5.0 (compatible; Baiduspider/2.0; +http://www.baidu.com/search/spider.html)" http://hk.wangxian.me/
    
    比较返回结果中 #index.panel > ul 文章列表UL中的内容；
    
后记：虽然这样做，不用定义特殊模板来渲染给Spider，但phantomjs较慢，\\    
可以在用缓存的方式解决，蜘蛛也不会每时每刻都去访问你的站点，是吧；

写完收工了! (写一篇技术文，还真累！)

---
（配图来自Bing）

- demo url <http://hk.wangxian.me>
- seed github url <http://github.com/wangxian/seo-express-seed>
