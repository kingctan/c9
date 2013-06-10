服务架构
---------------------------

主要的基类

* BaseService 处理单一model的crud
* FormService 处理单据的crud

BaseService
===============================


读取关系
========================

对于类似/api/sale_orders/1/sale_order_lines 这样的请求,系统会向BaseService调用read_realtion方法

read_relation(self, id, relation, relation_id, params=None)

如果你的服务类提供了同名的方法如sale_order_lines 则系统会调用该方法,并传递 id, relation_id, params 参数 (relation当然不用)

否则,系统根据id 获取记录,然后调用sale_order_lines属性

如果同时提供relation_id, 则系统从sale_order_lines中取一个值 (这是没有效率的方式, 仅仅是补完的需要)




.. rubric:: read_id(self, id=None, params=None)

读取类似/api/sale_orders/1

1. _read_id_q(self, session, id, params)
2. _read_q(self, session)
3. _read(q)
4. filter_by(id=id)





.. rubric:: __init__(self, user, method, set_of_book)

构造函数

.. rubric:: action方法签名

action 方法通常调用格式如下,如 /api/repairs?action=install::

	def install(self, id=None, parmas=None):
		pass

.. rubric:: update(self, id, params) 方法		

_update(self, session, upd, params)

可以覆盖该方法, 该方法session.add前执行, 过程

1. 更新upd属性
2. 设置updated_at,updated_user
3. 更新help_code,如果存在
4. 如果有保存方法,调用model.save


.. rubric:: create(self, params) 方法

_create(self, session, ins, params)

 可以覆盖该方法,该方法逻辑

1. 更新ins属性
2. 设置created_at,created_user
3. 更新help_code,如果存在
4. 如果有保存方法,调用model.save




.. rubric:: delete(self, id) 方法

该方法传入model的id

_delete(self, session, ins)

可以覆盖该方法，检查删除逻辑, 参考 RoleService的_delete方法, 该方法无需return::

    def _delete(self, session, ins):
        user_role = session.query(UserRole).filter_by(role_id=ins.id).first()
        if user_role:
            raise Exception(u'该角色存在用户,为避免误操作, 请先移除用户再删除')
        super(RoleService, self)._delete(session, ins)
