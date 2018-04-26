1. 需求：需要跨域请求后台的接口

```
#user  nobody;
worker_processes  1;   #允许执行的进程数，默认1

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

    upstream m_localhost{
        server scm.honglingjin.cn:9090;  #关键部分，   设置需要代理的接口地址
    }

    upstream z_localhost {
        server 192.168.197.205:9470;  #关键部分，   设置需要代理的接口地址
    }
    server {
        listen       80;  #真正请求的端口
        server_name  scm.honglingjin.cn;   #真正请求的域名  

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
        location / {   
            proxy_pass http://m_localhost;  # 当访问scm.honglingjin.cn时，访问的是这个代理前端地址 
        }

        location /scm-app-api { 
            proxy_pass http://z_localhost;  # 当访问scm.honglingjin.cn/scm-app-api时，访问的是这个代理接口地址 
        }

    location /daojia-document/backend-webui {
        root   html;
        add_header Access-Control-Allow-Origin *;
        add_header Access-Control-Allow-Headers X-Requested-With;
                  add_header Access-Control-Allow-Methods GET,POST,OPTIONS;
        add_header Cache-Control no-store;  
    }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

    }

}


2. 上线的Nginx  hash的情况
```

```
server {
    listen          80;
    server_name     hlj.rainbowcn.com;
#    root            /data/wwwroot/oa.gw-ec.com/oa/public;
    root            /hlj/app/scm;
#    access_log      logs/oa.gw-ec.com-access.log main buffer=32k;

#      fastcgi_param ENV_TYPE "dev";
#      fastcgi_param DOMAIN "ifelsend.com";
    location ~ ^/favicon\.ico$ {
      log_not_found off;
      access_log off;
    }
    location ~ ^/robots\.txt$ {
      allow all;
      log_not_found off;
      access_log off;
    }

    location /scm-admin/ {
#        alias /hlj/app/scm/scm-admin;
        index   index.html index.php;
        try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
        fastcgi_pass   def_php-fpm;
#        fastcgi_pass   unix:/hlj/server/php/var/run/www.sock;
        fastcgi_index  index.php;
        include        fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param SERVER_NAME $http_host;
        fastcgi_ignore_client_abort on;
    }

    location ~ \.(swf|js|css|xml|gif|jpg|jpeg|png|bmp|ico)$ {
        expires 3d;
    }

#    location /app_logs/ {
#        autoindex on;
#        alias /data/wwwroot/oa.gw-ec.com/oa/logs/;
#        allow 10.37.0.0/16;
#        deny  all;
#    }
}


3 history的情况


    server {
        listen          80;
        server_name     scm.honglingjin.cn;
        root            /hlj/app/scm;

        location /scm-app/ {
            alias /hlj/app/scm/scm-app/;
            index   index.html index.php;
#            try_files $uri $uri/ /scm-app/index.html$is_args$args;
            try_files $uri /scm-app/index.html;
        }

        location = /favicon.ico {
            log_not_found off;
            access_log off;
        }

        location ~ \.php$ {
            fastcgi_pass   unix:/dev/shm/php-fpm-5328.sock;
            fastcgi_index  index.php;
            include        fastcgi_params;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_param SERVER_NAME $http_host;
            fastcgi_ignore_client_abort on;
        }

#        location ~ \.(swf|js|css|xml|gif|jpg|jpeg|png|bmp|ico)$ {
#            expires 3d;
#        }
    }
```



