---
layout: post
comments: true
title: "commit log of first word"
category: ""
tags: 
  - git
---
![](http://ww1.sinaimg.cn/mw690/493b785agw1egl6iq6gvzj20iw07emxw.jpg)

> 5.28日更新，大写关键词

俗话说『无规矩不成方圆』在提交代码到仓库（git或svn）中时，要遵循一定的格式，  
所有的log以固定的引导词开始，之后简明扼要的说明，然后空一行，写上详细的说明(非必须)，  
这样做的好处是，方便从commit log中知道本次提交做了什么变更， 不用再去diff文件，省时省力。

整理了一下常用的commit log引导词：

<del>
Added     ( 新增加的功能 )
Fixed     ( 修复bug )
Changed   ( 完成的任务，需求变更，任务发生变化 )
Updated   ( 完成的任务，由于第三方模块变化而做的变化 )
Improved  ( 功能改进，完善 )
Finished  ( 完成某项功能 )
Packaged  ( 客户端打包构建结果，并标记版本号 )
</del>

从spmjs github上看到关键词都是大写的，遂觉得关键词大写，更容易区分。  
故都改成大写了。


    ADDED     ( 新增加的功能 )
    FIXED     ( 修复bug )
    CHANGED   ( 完成的任务，需求变更，任务发生变化 )
    UPDATED   ( 完成的任务，由于第三方模块变化而做的变化 )
    IMPROVED  ( 功能改进，完善 )
    FINISHED  ( 完成某项功能 )
    PACKAGED  ( 客户端打包构建结果，并标记版本号 )
    
    
如果改的地方比较多，不能确认使用什么关键词，  
可以拆分成多个功能点进行提交。（git推荐的方式）

---
读一份好的git commit log，就像读一部长篇小说，一部鲜活的历史。