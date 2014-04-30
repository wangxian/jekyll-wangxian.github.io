---

layout: post
title: "A go development tools - gorun"
comments: true
category: "go"
tags:
  - Go

---

<img class="cover" style="width:30%;"
src="http://ww2.sinaimg.cn/small/493b785ajw1e76b6xtkwkj205c07a0so.jpg" 
/>

Golang 开发不像PHP开发那么方便，经常要进行`CTRL+C`，然后重新运行，  
在搞nodejs开发的时候，经常用`nodemon`来自动重启nodejs app, 
找了一下，没发现好用的go auto restart app工具。

遂计划开发一个这样的工具，这就是`gorun`  
托管的项目地址：<https://github.com/wangxian/gorun>

# Usage:

	// 运行一个文件
	gorun gofile.go

	// 运行项目
	cd your_project_dir;
	gorun

# Installation
	go get -u github.com/wangxian/gorun