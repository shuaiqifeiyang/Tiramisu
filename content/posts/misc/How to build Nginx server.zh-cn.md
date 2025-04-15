---
title: "搭建Nginx服务器"
date: 2019-07-25T19:08:14-07:00
tags: ["Nginx", "博客搭建"]
categories: ["Misc"]
draft: false
---
在服务器上面安装配置Nginx
<!--more-->

## 安装Nginx

更新ubuntu软件源

```
sudo apt-get update
```

安装nginx

```
sudo apt-get install nginx
# 检查是否安装成功
nginx -v
```

**安装好了的文件的位置**

* /usr/src/nginx :主程序

* /etc/nginx :存放配置文件

* /usr/share/nginx :存放静态文件

* /var/log/nginx :存放日志

## 配置Nginx
 这部分主要是关于两个Nginx的配置文件的问题

/etc/nginx/nginx.conf
这个文件有默认配置，我们需要做一点修改
```nginx
# 这个文件有默认的配置
user root; #这个root很重要！
worker_processes auto;
pid /run/nginx.pid;

events {
	worker_connections 768;
	# multi_accept on;
}

http {

	##
	# Basic Settings
	##

	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;
	# server_tokens off;

	# server_names_hash_bucket_size 64;
	# server_name_in_redirect off;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	##
	# SSL Settings
	##

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
	ssl_prefer_server_ciphers on;

	##
	# Logging Settings
	##

	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;

	##
	# Gzip Settings
	##

	gzip on;
	gzip_disable "msie6";

	# gzip_vary on;
	# gzip_proxied any;
	# gzip_comp_level 6;
	# gzip_buffers 16 8k;
	# gzip_http_version 1.1;
	# gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

	##
	# Virtual Host Configs
	##
    # 需要加上我们的配置文件所在的目录
	include /etc/nginx/conf.d/*.conf;
	#include /etc/nginx/sites-enabled/*;
}

#mail {
#	# See sample authentication script at:
#	# http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
# 
#	# auth_http localhost/auth.php;
#	# pop3_capabilities "TOP" "USER";
#	# imap_capabilities "IMAP4rev1" "UIDPLUS";
# 
#	server {
#		listen     localhost:110;
#		protocol   pop3;
#		proxy      on;
#	}
# 
#	server {
#		listen     localhost:143;
#		protocol   imap;
#		proxy      on;
#	}
#}

```
/etc/nginx/conf.d/default.conf  
在之前的文件include了这个文件，这个文件里的配置是核心配置
```nginx
server {
	listen	80;
	server_name **.**.***.***;

	location / {
		root /usr/share/nginx/html/pc; #把请求转到这个目录
		index index.html
		allow all;	
	} 
	location ~/api/ { #把请求转到后端
		proxy_pass http://**.**.***.***:8080;
	}

	location ~/livecode/ {# 配置websocket
		proxy_pass http://**.**.***.***:8080;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection "upgrade";
	}	
}


```
## nginx常见操作

```
nginx #启动nginx服务
nginx -s stop #强行停止nginx服务
nginx -s quit #完成一些任务后停止nginx服务
nginx -t #检查nginx配置是否正常
nginx -s reload #重启nginx服务
netstat -tnlp #查看端口占用情况
```


