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