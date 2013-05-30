更新日志
------------------------

.. rubric:: 2013-5-29

* 合作伙伴增加移动电话

.. rubric:: 2013-5-28

* 现金银行变动 名称/拼音框生效, 并允许按科目代码搜索


.. rubric:: 2013-5-27

* 禁止移动浏览器 缩放
* 将编号/名称/拼音的编号去掉

.. rubric:: 2013-5-26

* 移动刷新缓存到工具条
* 增加memcached 支持
* 登录下载缓存从memcached下载, 刷新缓存会清除memcached缓存,也就是现在刷新缓存会真正的起作用
* 为一些模型定义增加passive_deletes=True 这样在删除时如果有引用则会提示错误


.. rubric:: 2013-5-23

* app_gevent 处理gevent异常
* 增加区域时刷新整个列表

.. rubric:: 2013-5-22


* 新增角色时 不显示角色用户和权限
* 删除角色时检查user_roles表
* 角色名称唯一性设置，通过对字段name设置unique=True

.. rubric:: 2013-5-16

1. 现在可以在model.save falure 回调中在operation中使用responseText了
2. 用户现在检查name/employee_id, 检查name唯一性，ad_name 绑定唯一性