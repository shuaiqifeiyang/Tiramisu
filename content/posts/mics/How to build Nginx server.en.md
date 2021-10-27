---
title: "How to build a Nginx server"
date: 2019-07-25T19:08:14-07:00
tags: ["Nginx"]
categories: ["Misc"]
draft: false
---
How to install and config Nginx in your server.
<!--more-->

## Installing Nginx

```
sudo apt-get update
sudo apt-get install nginx
# Check if the installation is successful
nginx -v
```

**Some folders about Nginx**

* /usr/src/nginx : main program

* **/etc/nginx : store config files**

* /usr/share/nginx : store static files

* /var/log/nginx : store log

## Configuring Nginx
This section is about config files.

/etc/nginx/nginx.conf
Some default content is in the file. We need to make some changes to this file.  
*   Change the first line to "user root"
*   In http block, add "include /etc/nginx/conf.d/*.conf;"
```nginx
user root; #!!this line is important
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
    # !!add the config file we write!!
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
We have included this file in /etc/nginx/nginx.conf. This file is our core configuration where we associate the path in the URL with the folder on the server.
```nginx
server {
	listen	80;
	server_name **.**.***.***;

	location / {
		root /usr/share/nginx/html/pc; #Forward the request to this directory
		index index.html
		allow all;	
	} 
	location ~/api/ { #Forward the request to backend
		proxy_pass http://**.**.***.***:8080;
	}

	location ~/livecode/ {# configure websocket
		proxy_pass http://**.**.***.***:8080;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection "upgrade";
	}	
}


```
## Nginx common commands

```nginx
nginx #start nginx service
nginx -s stop #stop nginx service immediately
nginx -s quit #stop nginx service after it finishes current tasks
nginx -t #check the configuration of nginx is valid
nginx -s reload # restart nginx service
netstat -tnlp # view port occupancy
```


