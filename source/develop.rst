开发
------------------


需求
====================

* ubuntu
* postgresql 9.2



安装
==========================


* virtualenv c9
* cd c9/source bin/activate
* git clone from bitbucket (c9webserver/c9cyclonewebserver/c9chatserver/c9cyclonechatserver/c9/docs)
* bin/pip install -r requirements.txt
* cd c9webserver/ ../bin/python c9webserver/app.py
* cd c9/../bin/python pyzmq.py
* cd c9chatserver/ ../bin/python chat_server.py


其它
==============================

搜索表达式
^^^^^^^^^^^^^^^^^^^^^^^^^^

c9 允许从客户端发起查询， 可以使用model__field__查询条件，其中model__部分通常不使用，一般就是field__查询条件, 如name__contains, 如果需要通过or查询多个字段, 可使用如下模式 name__contains__or__ad_name__contains__or__help_code__contains