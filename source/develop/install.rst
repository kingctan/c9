开发环境建立
-------------------------

需求
====================

* ubuntu/debian
* postgresql 9.2 参考 http://www.yuyaoe.com/topic/49


安装
==========================
* sudo apt-get install build-essential python-all-dev python-setuptools
* sudo easy_install virtualenv
* mkdir c9;cd c9
* virtualenv python
* source python/bin/activate
* git clone from bitbucket (c9webserver/c9cyclonewebserver/c9chatserver/c9cyclonechatserver/c92/c9.docs)
* cd docs;pip install -r requirements.txt
* 在c9webserver 目录 , python app.py
* 在 c9 目录, python pyzmq.py
* 在 c9chatserver目录, python chat_server.py


..rubric:: tornado/pyzmq 版本 

6.2 tornado 3.0.2 /from github source build pyzmq

初始化
=====================================

1. createdb c9
2. python scripts/init.py
