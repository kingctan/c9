更新日志
------------------------

*2013-5-22*

* 新增角色时 不显示角色用户和权限
* 删除角色时检查user_roles表
* 角色名称唯一性设置，通过对字段name设置unique=True

*2013-5-16*

1. 现在可以在model.save falure 回调中在operation中使用responseText了
2. 用户现在检查name/employee_id, 检查name唯一性，ad_name 绑定唯一性