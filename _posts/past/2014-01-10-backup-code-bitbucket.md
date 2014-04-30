---

layout: post
title: "backup your private code"
comments: true
category: weeklog
tags: 
  - weeklog
  - 开发

---

> 经常我们会写一些代码（非项目代码）来测试一些功能，或者演示demo，或不能公开的项目等等，
> 常年积累会越来越多，备份问题就很麻烦，
> 因为不独立项目，里面有关键数据，帐号等，不能push到Github上，比较愁人。

前段时间因为操作失误，把部分比较重要的代码给删除了，真是彻夜未眠，\\
多亏了`WondershareDataRecovery`全盘扫描，最后完美的恢复回来了。 虽然电脑上的`Time Machine` \\
一直开着, 但本地的`Time Machine`根据硬盘的大小，保存的时间不是很长。

所以就有了把代码备份到云上的想法，首先考虑的是Github，但Github仓库都是Public的，无意间发现了`Bitbucket`
这个和Github类似，但：

1. 支持无限Private库
2. 不限制使用硬盘大小
3. 支持Mercurial&Git
4. 支持自定义域名

尤其是前两点，简直就是给我备份代码准备的呀。 第三点支持Mercurial也很有意思，\\
在备份代码的时候，如果里面某个目录是git项目，可是使用Mercurial， 这玩意儿和git很像，使用 `hg` 来操作 \\
基本上和git命令一样，轻松上手，实在不行，安装`SourceTree` GUI操作，支持hg, git库，并SourceTree和Bitbucket \
是一个公司出品的。

用户我就不说了，几乎和Github一样，更神奇的是，你可以使用Github帐号登录，\\
并且可以把你的Github库导入到Bitbucket (不过开源库还是Github好些，毕竟兄弟姐妹们比较活跃嘛)

**参考链接：**

- Bitbuck WebSite <https://bitbucket.org>
- Free plan intro <https://bitbucket.org/plans>
- SourceTree Download <http://www.sourcetreeapp.com>

后记：\\
还有人说，把代码备份到百度云等空间，但这些不能查看代码，不能高亮；
