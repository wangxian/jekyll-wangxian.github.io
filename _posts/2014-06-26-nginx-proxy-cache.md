---
layout: post
comments: true
title: "nginx proxy cache"
category: ""
tags: 
  - nginx
  - jekyll
---

因为网站使用jekyll托管在github pages上，迁移到国内后使用nginx proxy的方式，  
但是速度还是很慢，后发现可以使用nginx_cache的来解决。

nginx_cache早已经内置在nginx的稳定版中，只要在配置的时候，指定就行了。
具体步骤：  

第一步：在server外配置

~~~
# 注：proxy_temp_path和proxy_cache_path指定的路径必须在同一分区
proxy_temp_path /data0/proxy_temp_dir;

# 设置Web缓存区名称为cache_one，内存缓存空间大小为200MB，
# 1天没有被访问的内容自动清除，硬盘缓存空间大小为30GB。
proxy_cache_path /data0/proxy_cache_dir levels=1:2 keys_zone=cache_one:200m inactive=1d max_size=5g;
~~~

第二步：在server内指定proxy_cache 和 proxy_cache_key

~~~
location / {
  proxy_pass http://wangxian.me/;

  proxy_cache cache_one;
  proxy_cache_key $host$uri$is_args$args;

  proxy_redirect off;
  proxy_set_header X-Real-IP $remote_addr;
  proxy_set_header REMOTE-HOST $remote_addr;
  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  proxy_set_header Cookie $http_cookie;
  
  # ... 其他代理的配置
} 
~~~

这样在浏览的的时候，nginx就会缓存。  
如果更新了网站要清理缓存，需要去/data0/proxy_cache_dir目录删除所有缓存，  
那能不能按照URL去更新呢？答案是肯定的，这个第三方的模块叫 `ngx_cache_purge`

### 安装 ngx_cache_purge

~~~
1. 下载：
wget http://labs.frickle.com/files/ngx_cache_purge-2.1.tar.gz

2. 解压

3. 配置
./configure --user=www --group=www --prefix=/usr/local/nginx \
--with-http_stub_status_module --with-http_ssl_module \
--with-http_gzip_static_module \
--with-ipv6 --add-module=../ngx_cache_purge-2.1 \

4. 安装
make && make install

5. 配置nginx

# 用于清除缓存
# 如果清理 http://wangxian.me/archive.html 缓存，
# 访问 http://wangxian.me/purge/archive.html 就可以清理缓存了
location ~ /purge(/.*) {
    # 设置只允许指定的IP或IP段才可以清除URL缓存。
    allow 127.0.0.1;
    allow 192.168.0.0/16;
    deny all;
    proxy_cache_purge cache_one host$1$is_args$args;
}    
~~~

是不是觉得速度快多了。

### 参考网站

- <http://wiki.nginx.org/HttpProxyModule>
- <http://wiki.nginx.org/CachePurgeChs>
- <http://zyan.cc/nginx_cache/>



