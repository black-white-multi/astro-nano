---
title: "Nginx"
description: ""
date: "2024-09-01"
tags: ['Nginx']
draft: false
---

## Ubuntu安装Nginx

sudo apt install -y nginx  

sudo systemctl start nginx  

sudo systemctl reload nginx  

sudo systemctl status nginx  

sudo systemctl restart nginx  

~~~sh
server {
    listen 8203;
    server_name localhost;
    location / {
        root /var/www/html/dist;
        try_files $uri $uri/ /index.html;
    }
}
~~~

反向代理  

~~~sh
location ~ / {
    proxy_pass http://IP:8203;
}
~~~

## Https配置

使用阿里云域名的SS证书  
申请证书blog.blackwhite.fun  
下载.pem文件与.key文件  
上传至服务器/etc/nginx/cert/  
修改配置文件/etc/nginx/sites-enabled/default  

~~~sh
server {
    listen 443 ssl default_server;
    listen [::]:443 ssl default_server;

    ssl_certificate "/etc/nginx/cert/blog.blackwhite.fun.pem";  
    ssl_certificate_key "/etc/nginx/cert/blog.blackwhite.fun.key";

    server_name blog.blackwhite.fun;
}
~~~

nginx -t  


