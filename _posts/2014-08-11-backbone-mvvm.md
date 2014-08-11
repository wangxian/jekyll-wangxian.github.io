---
layout: post
comments: true
title: "backbone.vm begining"
category: "JavaScript"
tags: 
  - JavaScript
---

正在开发一个MVVM Module, 基于Backbone, 名称：[backbone.vm](http://github.com/wangxian/backbone.vm)  
实现 Backbone.Model 和 HTML DOM的双向数据绑定；兼容Chrome*/IE6+/Safari...

# 1. Why New MVVM?

为什么要开发一个MVVM？ 原因很简单，眼馋Angular.js的方便，但讨厌其复杂规则，冗余  
的功能设计，不可控性高，性能低，且在国内不支持老浏览器(虽然可以经过特殊的手段可以支持，但...)

实际工作中Backbone的使用最广泛，且比较灵活，考察了一下国内外MVVM库，  
暂无比较好用的解决方案（angular.js/backbone.stickit/avalon.js/Knockback.js）考虑过
是基于现有的轮子再造轮子，还是造一个新轮子，avalon.js从零造了一个新轮子，成本较高也较复杂。
如果是现有的基础上，省去了很多问题，但也带来了别的问题，如依赖多。

功能的实际上，简单，实用就够了。 对于节点属性选择上，只增加一个节点属性vm="val:username", 
不提供xx-controller, xx-html等标记，所有的都放到vm属性里，对于控制器（或VM的作用范围）
在定义VM类时指定，VM类初始化的时候，进行扫描节点, 建立DOM VIEW和MODEL的双向映射关系。

不使用对象监听属性变化，直接使用Backbone.Model来存储VM, 好处是不用做兼容，现成的。  

这样，简单、高效、上手快、兼容多浏览器，不是难事儿！

# 2. Feature List

1. 视图和数据的双向绑定
2. 兼容性 Chrome*/IE6+/Safari
3. 操作方法直接使用jQuery关键字，html, val, text...
4. 依赖库可使用jQuery/Zepto, Underscore/lodash替换

# 3. Timeline

- 基本功能开发(进行中)
- 兼容性检查
- 代码优化
- 文档完善
- 功能示例完善
- 发布到spm
- 修改BUG
- 功能增强
- 迭代


------------------------
相关链接：

- github repo <https://github.com/wangxian/backbone.vm>
- spm doc <http://spmjs.io/docs/backbone.vm/latest/>






