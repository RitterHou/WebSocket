聊天的前台界面，默认即会访问 [index.html](index.html) 页面，以下为 Nginx 的配置：

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
	        proxy_read_timeout   300s; # Nginx 的 WebSocket 超时配置，默认 60s 自动断开链接  
	        proxy_set_header     Upgrade $http_upgrade;
	        proxy_set_header     Connection "upgrade";
	    }
	}

备注：如果页面本身使用的是 HTTPS 协议，那么只需要把 WebSocket 连接的协议从 ws 改为 wss 就可以了。