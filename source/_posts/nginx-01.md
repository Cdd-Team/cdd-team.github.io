---
title: Nginx无法挂载/root目录的静态资源
toc: true
date: 2020-02-04 19:56:51
tags:
- Nginx
categories:
- web部署
- nginx采坑
---



### nginx静态资源文件无法访问，403 forbidden错误

在安装 nginx 服务器后，我想把网站的根目录设置为 `/root/www/` ，于是对 `nginx` 的 `nginx.conf` 文件进行配置

<!--more-->

先打开 `nginx.conf`

```
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;
    
        charset utf-8;
    
        #access_log  logs/host.access.log  main;
    
        location / {
            root   /root/www/;          ## 设置的地方
            index  index.html index.htm;
        }
        #error_page  404              /404.html;
    
        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
        		root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
}
```

保存后，重启 nginx 服务，然后出现了 403 错误

### 解决方案



网上查询后说是权限问题，更改 nginx.conf 的第一行
将 `#user nobody;` 改为 `user root;`

保存，再次重启 nginx 服务，访问成功

![nginx-root.png](https://i.loli.net/2020/02/04/gSbe6TniEx5hBdu.png)

如果不想使用root用户运行，就不能把目录放在 `/root/` 目录下了，可以选择放在 `/home/www` 下，并设置 www 的权限 777，同样可以访问成功。
![nginx-home.png](https://i.loli.net/2020/02/04/fYeEpcF7qbQJSW2.png)



## 参考资料
> - []()
> - []()
