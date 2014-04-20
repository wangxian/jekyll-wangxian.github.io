---
layout: post
title: "Angular.js学习笔记与感悟"
category: "JavaScript"
comments: true
---


Angular.js是google出品的一个非常牛x的前端MVC框架，详细的介绍你可以
[百度一下](http://www.baidu.com/s?wd=angular) 。

2013年春节，放假8天，吃了睡，睡了吃的事情，不能让脑子荒废了，如果脑子生锈了，那怎么
拿来上班，哈哈。

花了3天时间细心的研究了angular，怎么觉得名字像“安哥拉”
版权写的也比较有个性“Super-powered by Google ©2010-2012 ( v1.0.3 bouncy-thunder )”
看到这个版权，你或许知道你怎么选择了，文档写的还是非常详细的。从github上看到源码中既有nodejs，也有ruby，
真是google的风格呀；

教程性的东西，我就不写了，angular写的已经够详细的。angular最牛x的是她的 Testacular 测试，太棒了。
单元测试和端对端测试。

用angular写应用非常简单，js的部分非常少，控制器，模型和视图完全分开，filter ,module （和seajs的module补一个概念）
router, $http, form valid, jqlite, multiple view, rest custom service;

#### 下面对这些方面说一下我的理解：
--------------------------------------

> 1. 模型、控制器、视图分离分开很有必要，对服务的封装，让angular用这个更像一个app的高层应用,
> 这是一个优点，同时也算是一个缺点，对底层过于封装，太过于严密，比如没有events层，
> 这对于mvp基于事件的应用就不太适合, 如果做本地应用就不适合。angular偏向于网络http的WebApp；
>
> 2. filter 很好，很强大，view层表达式，不允许写表达式，angular认为这是controller的工作，要求很严格。写了就执行错误。
> 3. angular宣讲自己是声明式，其他的命令式的
> 4. moudle 创建太过抽象，对于控制器作用域， 操作起来很麻烦，对于英文文档上的解释（看着很费劲，构造器apply，
> 但是对于注入的全局, $watch的原理还不是很明白。如何让自定义事件去改变模型数据，比如webapp的tap, singleTap, swipe, 文档没写）
> 所以angularjs 还是偏向于网络应用，如果是桌面应用(webview执行)，本地执行file:/// 就一些功能就非常费劲了，
> 还有虽说视图和model双向绑定，但是在控制器中，如何方便的操作model来改变view，
> 可能我对service的理解还不够深入。总觉得用起来力不从心。
>
> 5. angular极度讨厌全局；
> 6. angularjs执行ie8以上浏览器，ie8一下浏览器需要兼容。
> 7. url router 这个也非常棒，支持老浏览器和html5新的特性。pushState和hashbang
> 8. 内置http, dom element 请求，不用依赖jquery, 有简化版的jqlite
> 9. form valid 内置表单验证，ie的兼容性，我没测试。
> 10. multiple view 多视图，视图片段，这个很多服务器端开发经常用的功能，布局视图，但问题来了，加载别的视图，
>     需要用到ajax去加载，让桌面webview 或 hybird WebApp 增加了不确定性。
> 11. rest custom service 简化服务，看清楚，不是rest url, tutorial上演示简化ajax 但这个功能用处不大。
> 12. 还是需要events层，前端嘛，还是基于各种事件。
> 13. 能看到某些xx服务器端开发语言的特性。

# 总结
Angular.js还是一个新生事物，对于本地应用还有些局限，如果能在这2个方面，
得到改善，那就完美了! 期待少一些xx语言的影子，多些javascript本身的特性。



