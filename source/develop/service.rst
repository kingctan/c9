服务架构
---------------------------

主要的基类

* BaseService 处理单一model的crud
* FormService 处理单据的crud

BaseService
===============================

.. rubric:: __init__(self, user, method, set_of_book)



.. rubric:: delete(self, id) 方法

该方法传入model的id

_delete(self, session, ins)

可以覆盖该方法，检查删除逻辑, 参考 RoleService的_delete方法, 该方法无需return::

    def _delete(self, session, ins):
        user_role = session.query(UserRole).filter_by(role_id=ins.id).first()
        if user_role:
            raise Exception(u'该角色存在用户,为避免误操作, 请先移除用户再删除')
        super(RoleService, self)._delete(session, ins)