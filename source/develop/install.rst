开发环境建立
-------------------------

需求
====================

* ubuntu/debian
* postgresql 9.2 debian参考 http://www.yuyaoe.com/topic/49


安装
==========================
* sudo apt-get install build-essential python-all-dev python-setuptools
* sudo easy_install virtualenvwrapper
* 编辑.bashrc 增加 source /usr/local/bin/virtualenvwrapper.sh
* mkvirtualenv c9
* mkdir c9;cd c9
* workon c9
* git clone from bitbucket (c9webserver/c9cyclonewebserver/c9chatserver/c9cyclonechatserver/c92/c9.docs)
* cd docs;pip install -r requirements.txt
* 使用tornado 在 c9webserver 目录, 运行  python app.py conf/xxx/app.json
* 使用cyclone, 在 c9cyclonewebserver, 运行 python app.py conf/xxx/app.json
* 在 c9 目录
  * 纯pyzmq 运行, python pyzmq.py conf/xx/pyzmq.json 
  * gevent 运行,  python app_gevent.py conf/xx/app_gevent.json 
  * twisted 运行, python app.py conf/xx/app.json
* tornado+socket.io 在 c9chatserver目录, python chat_server.py conf/xxx/chat_server.json
* twsited_sockjs, 在c9cyclonechatserver, python chat_server.py conf/xxx/chat_server.json


..rubric:: tornado/pyzmq 版本 

6.2 tornado 3.0.2 /from github source build pyzmq

初始化
=====================================

1. createdb c9
2. python scripts/init.py
