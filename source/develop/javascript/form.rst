表单
-------------------------------


C9.form.BaseForm
===========================

所有表单的基类

.. rubric:: 约定

* 明细grid命名为line_grid
* 动作grid命令为action_grid
* 窗体命名为form,第二个命名为form2
* 组合line_grid/action_grid的tab命名为line_tab
* 多个窗体的tab命名为form_tab

.. rubric:: 属性

用户是否能编辑必须符合以下条件 status不等于6并且owner为true

.. code-block:: javascript

	me.status === 6 || !me.owner


* status - 表单状态, 6 约定用于完结， 缺省undefine, 该属性在loadFromRecord和loadNewRecord中调用SetFormReadOnly时设置
* owner - 是否所有者， 当loadNewRecord为true, loadFromRecord根据updated_user和created_user判断， 缺省true


.. rubric:: 方法

setFormReadOnly

子类覆盖此方法设置是否将改该表单设为只读或取消只读