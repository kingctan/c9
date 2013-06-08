c9 chat server
-----------------------

例子::

	{
	
		"NAMESPACE":"socket.io",
		"COOKIE_SECRET": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
		"SSL_OPTIONS": {
		 	"certfile": "c:/c92/certificate/server.crt",
	        "keyfile": "c:/c92/certificate/server.key"
	  	}
	}


配置项
========================================	

* NAMESPACE  使用 /socket.io路径请求
* COOKIE_SECRET cookie加密所有的SECRET 必须同c9webserver的设定一致,更新COOKIE_SECRET时请同步更新
* SSL_OPTIONS 如果c9使用https方法,在此处同时配置c9chatserver也使用同样的证书使用https访问