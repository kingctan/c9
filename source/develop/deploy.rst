部署
-----------------------------------

自 2013/6/7起,在所有平台均使用virtualenv发布形式, 放弃cx_freeze/py2exe之类的打包形式(除了windows下的nginx_service, 因为他依赖服务停止时发出-s stop命令)

部署根目录按c9+版本号形式,如 0.2 版本为c92, 0.3 版本为 c93, 以后类推


windows 部署
========================================

windows 下主要依赖srvany.exe来做windows services 管理

.. rubric:: 目录结构


* c9 - c9 application server
* proxy - c9 proxy 服务
* c9webserver - c9 webserver 
* c9chatserver - 聊天服务 
* fonts - 字体文件, pdf 打印时用
* templates - 模板
* static - 静态文件
* nginx-1.5.1 - nginx
* certificate - 证书
* pg_dump_service postgresl 备份服务
* nginx_service - nginx 服务 , linux不需要
* memcached-win32-1.4.4-14 
* backup 备份目录
* logs 日志目录
* env virutalenv
* conf 配置文件


nginx_service/proxy 各会占据一个console windows host进程


.. rubric:: 需求

* 安装python 2.7.4

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
* 删除c9[version] 目录

.. rubric:: 分发

1. 更新static/js/app/bootstrap.js VERSION
2. 更新 c9/c9/settings.py VERSION
3. 运行deply.sh/deply.bat
