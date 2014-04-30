---

layout: post
title: "installing github pages"
comments: true
category: weeklog
tags: 
  - weeklog
  - jekyll
  - Github

---

最近发现使用 `github-page` 来安装Jekyll，可以保持本机的Jekyll和github pages的包版本一直。
再也不用担心，不小心升级jekyll包，导致和github pages 不兼容了。

该方法是gitub官方提供的方法:

本地新建一个 `Gemfile`


    source 'https://rubygems.org'
    gem 'github-pages'

然后运行 `bundle install` , 然后等着就行了。

如果未创建Gemfile,也可以直接运行 `gem install github-pages` 来安装。

如果要升级，运行：`bundle update` or `gem update github-pages`

# 参考：
- [Using Jekyll with Pages](https://help.github.com/articles/using-jekyll-with-pages)
- [Quick Reference of kramdown](http://kramdown.rubyforge.org/quickref.html)
