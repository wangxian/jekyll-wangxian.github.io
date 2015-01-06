---
layout: post
comments: true
title: "gitlab install"
category: ""
tags: 
  - git
---

说实在，gitlab的体验真是不错，安装也挺简单，就是有一点运行需要的内存不小，512M内存都无法运行。
以阿里云 CentOS6 为例简单的说一下安装过程。 

## 一、下载社区版 Gitlab安装包
  
gitlab比较厚道，社区版已经够用了，下载地址：https://www.gitlab.com/downloads/
文件名名称类似gitlab-x.y.z.rpm
  
## 二、安装

    sudo yum install openssh-server

    // sendmail or exim is also OK
    sudo yum install postfix     
    sudo rpm -i gitlab-x.y.z.rpm

    // 设置gitlab访问URL
    vim /etc/gitlab/gitlab.rb
    external_url "http://git.xxxx.com"

    // 初始化配置
    sudo gitlab-ctl reconfigure

    // 启动postfix
    sudo service postfix start

初始化配置可能比较慢，需要几分钟。完成后
打开浏览器，访问`http://git.xxxx.com`就可以了。

默认帐号`root`, 密码 `5iveL!fe`



## 三、关于postfix发邮件

gitlab默认可以发邮件，不需要SMTP配置，只要系统启动了postfix就行了。  
因为这个折腾了好久，配置smtp还是比较麻烦的，最后还是采用postfix发邮件。


## 四、关于80端口

默认gitlab自带nginx，使用80端口启动，如果要修改，把 `/etc/gitlab/gitlab.rb`
里的external_url 修改为http://git.xxxx.com:18080，\\
然后执行 sudo gitlab-ctl reconfigure

这样就可以使用已有的nginx来proxy gitlab了。

--------------------

其他版本的Linux，参考gitlab的官方Wiki 
<https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/README.md>



