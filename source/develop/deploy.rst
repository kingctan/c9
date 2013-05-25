部署
-----------------------------------

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

.. rubric:: 需求

* 安装 postgresql 9.2
* 安装vc 2008/2010 运行时

.. rubric:: 安装

* install_service.bat
* start_all.bat

