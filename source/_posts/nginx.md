### nginx配置前端打包后的代码----------------------------------
server {
	listen 		  8000;
	server_name	  localhost;

	location / {
		root    html/vue-anchor-admin;
		index   index.html index.htm;
	}
	location /api {
	      proxy_set_header Host wx.guanxiaohe.cn;
	      proxy_pass http://wx.guanxiaohe.cn/ssm;
	}
}


server {
    listen        8002;
    server_name   localhost;

    location / {
        root    html/vue-anchor-admin-iview;
        index   index.html index.htm;
        try_files $uri $uri/ /index.html;
    }
    location /api {
          proxy_set_header Host rap2api.taobao.org;
          proxy_pass http://rap2api.taobao.org/app/mock/122795;
    }
}