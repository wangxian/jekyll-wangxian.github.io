---
layout: post
title: "升级Openshif自带的Nodejs"
category: "PAAS"
comments: true
tags: PAAS

---

> 原因：Openshift自带的nodejs 为0.6.20 版本太老了
> 下面的步骤可以升级为自定义版本。
> 安全可靠，本人尝试成功；

cd your_project_dir
git remote add upstream -m master git://github.com/openshift/nodejs-custom-version-openshift.git


git pull -s recursive -X theirs upstream master

\~# 修改为你想安装的版本，比如：0.8.22
vim .openshfit/markers/NODEJS_VERSION

\~# push 到openshift
git push


等着就行了，执行结束，你的openshift的nodejs 就升级为你期望的版本了。