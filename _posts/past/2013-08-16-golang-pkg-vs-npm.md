---

layout: post
title: "Golang package manage VS NPM"
comments: true
category: weeklog
tags: 
  - weeklog
  - Go

---

<img src="http://ww4.sinaimg.cn/large/493b785ajw1e7r0qn9pqzj20a003wmx2.jpg" />

研究Go语言有段时间了（也叫Golang）现代的开发语言都有一个包管理，go也自带了一个包管理没有名字叫`go get`
Nodejs的包管理叫npm，go get虽然简单直接，但和Node.js npm 一比还是比较弱的，粗略的讲有3个方面。

+ 命令行使用上的差别
+ 版本管理
+ 仓库源

## 命令行使用上的差别

先说命令行使用，`go get` 命令，我已知有用的只有一个参数 `-u` 更新已安装的包。没有删除已安装的包命令，
不能查看第三方包的介绍，不能搜索你想要的包功能，等等，和npm一比简直是弱爆了。

**npm的功能**

    Usage: npm <command>

    where <command> is one of:
        add-user, adduser, apihelp, author, bin, bugs, c, cache,
        completion, config, ddp, dedupe, deprecate, docs, edit,
        explore, faq, find, find-dupes, get, help, help-search,
        home, i, info, init, install, isntall, issues, la, link,
        list, ll, ln, login, ls, outdated, owner, pack, prefix,
        prune, publish, r, rb, rebuild, remove, repo, restart, rm,
        root, run-script, s, se, search, set, show, shrinkwrap,
        star, stars, start, stop, submodule, tag, test, tst, un,
        uninstall, unlink, unpublish, unstar, up, update, version,
        view, whoami

## 版本管理

go的包，没有版号，当然goget也就没有了版本管理的功能，
对于npm每一个包，都有一个package.json文件描述该包，什么版本，该包依赖于那些包，
当你npm install的时候npm会把依赖的包安装上，更强大的是，包可以指定依赖包的版本。

如果包的依赖包没有版本，就需要使用者自己确认，如果依赖包升级后，可以导致包不能使用。

对于这些功能，goget，一个都冇，比起来，go还是很年轻。


## 仓库源
npm有一个官方的仓库<https://npmjs.org/> , goget没有，goget在线安装只能支持
有限的几个源 google code, github等。

没有官方源，也就不能统一管理，对包进行审核等，虽然现在npm也没有审核，但可以看到那些包是被使用和
下载最多的，这样大家认为好的，基本上可以确定是优质的包。

没有官方源只能靠你的一双慧眼了。


##### 总结
路漫漫其修远兮，吾将上下而求索。


