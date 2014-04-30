---

layout: post
title: "构建Android下开发WebApp环境"
category: "mobile"
comments: true
tags: 
  - 开发

---

>>> 后记：发现一个非常遗憾的事情，ucweb dev版是不能进行跨域访问的。
>>> 在开发中用了backbone的网络请求，也就不能完全使用ucweb dev调试了

下面记录一下我折腾出的开发 Hybrid APP 的开发环境。以便给还在路上的人，少走一些完了。
在ios平台下开发调试webapp相对比较简单，ios6 safari支持远程调试，详细的用法，可以搜索一下，配制比较简单，
可以用mac的safari链接模拟器或真机，基本上不用做额外的配制。

------------------------------------

### 模块加载器 seajs

seajs不仅是用来做模块加载器, seajs有一个插件 `plugin-reload` 我非常喜欢，可以解放双手来刷新来看到界面。
关于seajs plugin-reload 的使用和配制，情况seajs issue : <https://github.com/seajs/seajs/issues/224>

------------------------------------

### 摆脱pc chrome develop tools - 真机WIFI调试

感谢ucweb，为我们提供了远程调试的浏览器，ucweb的网站上有教程，<http://www.uc.cn/business/developer.shtml>
不过教程是以windows为蓝本的，mac上其实是一样可以的，不用ucweb官方提供的 `adb` 工具，使用android sdk tools上提供的
`adb` 即可。

- [UC浏览器开发者版使用手册(Android平台)](http://wap.uc.cn/index.php?action=PackageDown&do=ByPfid&product=UCBrowser&pfid=145&lang=zh-cn&bid=33533&direct=true&from=dev-slp-dir-pc)
- [ucweb android 开发包 apk](http://wap.uc.cn/index.php?action=PackageDown&do=ByPfid&product=UCBrowser&pfid=145&lang=zh-cn&bid=33533&direct=true&from=dev-slp-dir-pc)
- [Download the Android SDK](http://developer.android.com/sdk/index.html)

------------------------------------

### 开发工具推荐

- sublime text 2
- webstrom
- chrome