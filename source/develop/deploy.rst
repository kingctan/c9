部署
-----------------------------------

linux 打包 部署
==========================================

从0.2 开始, linux可以同windows 一样使用cxfreeze打包, app_gevent/c9webserver在linux下不打包zmq/gevent,通过手动复制包进行


linux virutalenv部署
==================================

* sh install_virtualenv.sh



windows 部署
========================================

.. rubric:: 目录结构

* application_server - c9 application server,按进程数(从1开始) 分多个子目录
* proxy - c9 proxy 服务
* webserver - c9 webserver 按端口号分多个子目录,默认从8000开始
* fonts - 字体文件, pdf 打印时用
* templates - 模板
* static - 静态文件
* nginx-1.4.1 - nginx
* certificate - 证书
* chat_server - 聊天服务
* pg_dump_service postgresl 备份服务
* nginx_service nginx 服务
* memcached-win32-1.4.4-14 
* backup 备份目录
* logs 日志目录

默认安装到c9盘


.. rubric:: 需求

* 安装 postgresql 9.2

通过远程桌面安装postgresql 9.2 可能会因为权限问题导致安装失败, 建议的方式是将postgres账户加入到本地管理员组,然后以postgres登录安装,然后再将其从本地管理员组中移出

* 安装vc 2008/2010 运行时

* 安装7zip 备份需要

.. rubric:: 安装

安装过程现在非常简单

* install_service.bat
* start_all.bat

卸载也只需要

* stop_all.bat
* uninstall_service.bat


