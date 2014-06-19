---

layout: post
title: "jekyll kramdown highlight"
comments: true
category: weeklog
tags: 
  - weeklog
  - jekyll

---

把Jekyll的markdown解析换为kramdown，主要的原因是kramdown支持像Github一样的代码块高亮写法。\\
今天折腾了好久，Google后发现不是Jekyll的问题，原来如果要使用

    ~~~ php
    phpinfo()
    ~~~

的代码高亮, 需要安装coderay。 找了半天文档，发现 <http://kramdown.gettalong.org/converter/html.html>
有这样一句。

    Note that syntax highlighting won’t work unless the CodeRay library is installed!
    
解决办法：

    gem install coderay
    
但是这还没完，完了发现 github pages 上没有安装coderay，只能作罢！（或者只能在本地编译好，然后传上去了 ..nojekyll）

# 参考：
- <http://kramdown.gettalong.org/converter/html.html>
- <https://help.github.com/articles/using-jekyll-with-pages>
- <http://coderay.rubychan.de/download>

