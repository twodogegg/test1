---
title: "Nginx 配置 ThinkPHP5 站点"
date: 2020-03-17T14:39:41+08:00
draft: true
slug: "nginx-config-thinkphp5-website"
tags:
  - nginx
  - thinkphp
---

## Docker 环境下的例子

```
server {
    listen       80;
    server_name  rhaphp.test ;
    root  /var/www/html/rhaphp;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";

    charset utf-8;

    index index.html index.htm index.php;
    location / {
        try_files $uri $uri/ /index.php$uri;

        if (!-e $request_filename) {
            rewrite  ^(.*)$  /index.php?s=/$1  last;
            break;
        }
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location  ~* .(jpg|gif|png|js|css|otf|mp3|mp4|m4r)$ {
	 root /var/www/html/rhaphp;
	  if (-f $request_filename) {
	   expires max;
	   break;
        }
    }

    location ~ \.php(.*)$ {
        fastcgi_pass   php:9000;
        fastcgi_index index.php;
        fastcgi_split_path_info  ^((?U).+\.php)(/?.+)$;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        fastcgi_param  PATH_INFO  $fastcgi_path_info;
        fastcgi_param  PATH_TRANSLATED  $document_root$fastcgi_path_info;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```
