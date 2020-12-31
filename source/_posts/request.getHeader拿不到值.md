---
title: request.getHeader拿不到值
date: 2020-12-30 23:47:44
categories: nginx
tags: nginx
---

## 问题

SpringBoot项目，部署在linux上，request.getHeader("access_token")一直无法取到值。

但是在本地windows环境下是没问题的

##  原因

归根究竟，是因为服务器上部署了nginx，**默认情况下header名字是不能加下划线的**

###### 根据nginx文档，是因为历史遗留原因

```
If you do not explicitly set underscores_in_headers on;, NGINX will silently drop HTTP headers with underscores (which are perfectly valid according to the HTTP standard). This is done in order to prevent ambiguities when mapping headers to CGI variables as both dashes and underscores are mapped to underscores during that process.https://www.nginx.com/resourc...
```

## 解决办法

##### 一、修改header值

将access_token改成access-token

#####  二、修改nginx配置

配置nginx的http，让它支持了下划线

```
underscores_in_headers on;  // 允许headers fields 里的下划线

    location / {
        proxy_pass_request_headers on; // 确定转化http headers

        proxy_pass_header Server;
        proxy_redirect off;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Scheme $scheme;
        proxy_connect_timeout 60s;
        proxy_read_timeout 5400s;
        proxy_send_timeout 5400s;
        proxy_pass http://pb_web;
    }
```

