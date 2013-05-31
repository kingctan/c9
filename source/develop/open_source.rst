开放源代码
==============================

C9 计划逐步开放源代码, 当然, 开放源代码不是目的, 主要的是为了C9的体系更加结构化,更加易于扩展, 同时,通过开放源代码这种外部作用力, 使代码更规范,更安全

C9 的0.3 版本将是一个第三方扩展完备的版本, 参考 :doc:`/develop/version`, 我们计划通过一个开源的 :doc:`/repair/index` 来验证这一点

当前

* C9 的文档, 开源, 参考 https://github.com/jiangjianxiao/c9
* C9 返修模块, 开源,正在开发中 https://github.com/jiangjianxiao/c9_repair
* C9 c proxy模块, 开源 https://github.com/jiangjianxiao/wuproxy

未来, 我们将逐步打碎C9, 逐步开放其销售,采购,库存,财务等模块, 最终到达全部开源的目的

从现在开始,凡是新开发的模块, 如商城接口,taobao 接口, 移动界面等,一开始就走开源的途径


.. rubric:: C9 的技术栈

* python/pypy
* tornado/twisted/gevent 对于Web server 我们准备了三套方案,对于应用服务,我们准备了基于twisted和gevent的方案
* zeromq/pyzmq
* postgresql/psycopg2
* sqlalchemy
* memchached
* reportlab/xlwt/xhtml2pdf/xldt/python-ldap等
* socketio/socketjs 支持
* 打包方案cx_freeze
* c/cython 部分使用