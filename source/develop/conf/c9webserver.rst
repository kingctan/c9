c9 web server
-----------------------------

例子::

    {
      "TEMPLATE_PATH": "c:/works/c92/c9/templates",
      "STATIC_PATH": "c:/works/c92/c9/static",
      "PYZMQ_URL": "tcp://localhost:5556",
      "DEBUG": true,
      "SSL_OPTIONS": {},
      "COOKIE_SECRET": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",    
      "EXTENSIONS": [{"package": "c9_repair", "bootstrap":"/static/js/c9_repair/bootstrap.js"}], 
      "RELEASE": false,
      "DEFAULT_SET_OF_BOOK": "c9",
      "SET_OF_BOOKS": [
        {
          "name": "c9",
          "text": "缺省帐套",
          "status": 1
        },
        {
          "name": "c92012",
          "text": "c9 2012帐套",
          "status": 2
        }
      ]
    }


配置项
=============================== 

* TEMPLATE_PATH 模板路径,绝对
* STATIC_PATH 静态文件路径, 绝对
* DEBUG - 当前,总是true
* SSL_OPTIONS - 当前不用设定, 当前,https由nginx实现
* EXTENSIONS - c9扩展配置
* RELEASE  - 不使用
* DEFAULT_SET_OF_BOOK 缺省账套
* SET_OF_BOOKS 账套列表, 每个项是个dict , name 对应 :doc:`c9`中的SET_OF_BOOK的key, text是该账套描述, status是表示账套是否处理启用或关闭状态
* COOKIE_SECRET - cookie 加密串 必须同c9chatserver.json配置一致, 用scripts/cookie_secret.py可生成

