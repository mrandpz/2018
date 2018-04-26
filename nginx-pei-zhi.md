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
        server scm.honglingjin.cn:9090;
    }

    upstream z_localhost {
        server 192.168.197.205:9470;
    }
    upstream adminapi_localhost {
        server 192.168.197.205:9480;
    }
    upstream admin_localhost{
        server scm.honglingjin.cn:9091;
    }

    server {
        listen       80;
        server_name  scm.honglingjin.cn;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
        location /scm-admin {
            proxy_pass http://admin_localhost;
        }
        location / {
            proxy_pass http://m_localhost;
        }



        location /scm-app-api { 
            proxy_pass http://z_localhost;
        }

        location /scm-admin-api { 
            proxy_pass http://adminapi_localhost;
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
```



