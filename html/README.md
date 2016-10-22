聊天的前台界面，默认即会访问 index.html 页面，以下为 Nginx 的配置：

	server {
	        
	    listen       80;
	    server_name  127.0.0.1;
	
	    location / {
	        root   html;
	        index  index.html;
	    }
	
	    location /ws {
	        proxy_pass           http://127.0.0.1:8080;
	        proxy_http_version   1.1;
	        proxy_set_header     Upgrade $http_upgrade;
	        proxy_set_header     Connection "upgrade";
	    }
	}