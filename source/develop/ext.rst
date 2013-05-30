扩展
-------------------------

鉴于并非在开发之初就考虑到扩展的可能,所以扩展的开发还在演进中

返修模块是扩展实现的例子, 参考 https://github.com/jiangjianxiao/c9_repair

服务端扩展
========================

服务端扩展基于当前服务端只看载入的服务类这一前提

1. 创建你自己的包,用c9_开头,如c9_repair, 建议包结构::

	c9_repair
		static - 你的静态文件
			js
				app
					repair.js
		templates - 你的模板文件
			moudles
				repair
					repair.html
		c9_repiar
			services
				__init__.py
				repair.py - RepairService
			workflows
				__init__.py - RepairWorklfow
			models.py sqlalchemy model
			__init__.py

		reamde.rst 说明文件


2. 修改你的 packages.__init__.py 暴露服务类, 注册工作流::

	from .services.repair import RepairService

	from .workflows.repair import RepairWorkflow

	from c9 import settings
	settings.WORKFLOW_FACTORY['repair'] = RepairWorkflow

	del RepairWorkflow
	del settings

3. 编辑配置文件, 增加 EXTENSIONS 设置 , 如::

	EXTENSIONS: [{"package":"c9_repiar", "bootstrap": "/static/js/c9_repair/bootstrap.js"}]

4. 创建security_keys/menu_items/menus, 创建工作流定义, 建议用脚本 todo 


客户端扩展
===========================


对于前端, 存在着两类文件, 一类是启动时就载入的js 文件, 最终这些文件会被压缩到一个c9_all.js 中,还有一些是模块,按需载入,这些文件是包含javascript的html文件(todo , 不好调试,无法正确定位出错行)

第一类文件,系统是通过一个bootstrap.js 文件载入的, 建议你参考该文件,做自己的一个module_bootstrap.js文件,处理启动时文件的载入, 配置中的bootstrap就是处理该事项

第二类文件, 你完全是自由的,当你定义menuitem时决定文件的位置

用ln -s 或  mklink 创建static/templates目录的符号链接

通常的步骤
^^^^^^^^^^^^^^^^^^^^^^^

* 定义model, 少许的话可以直接在bootstrap.js中定义, 多的话建议另开一个文件
* 有表单的话创建表单文件, 在bootstrap.js中载入并注册FORM_NEW_REC_MAP/FORM_CLASS_MAP, 参考下方
* 建立模块html文件
* 通过注册的menu/menu_item访问

表单
^^^^^^^^^^^^^^^^^^^^^^^^

C9中存在两种表单实例,一种是singleton形式的, 一种表单类型只存在一个实例,这些实例存在于form_holder(global.js), 操作方法是open_form/new_form(common.js), 还有是每次都打开一个新实例,关闭时destroy , 操作方法是open_new_form(common.js)

 当你新建一个表单时,需要向FORM_CLASS_MAP注册(建议你写在你的扩展的bootstrap.js文件中)::

 	FORM_CLASS_MAP['repair'] = 'C9.form.RepairForm';

并注册一个new_xxx的方法, 该方法用于提供缺省值::

	FORM_NEW_REC_MAP['new_repair'] = function {
		return new Repair({
			created_at: new Date(),
			employee_id: user.employee_id,
			employee_name: user.employee_name,
			department_id: user.department_id,
			department_name: user.department_name //,
			//store_id: user.default_store_id,
			//store_name: store_renderer(user.default_store_id)

		});

	}

发布你的扩展
=============================

.. rubric:: 打包发布的C9

将c9_reapir/c9_repair 目录复制到 application_server/[1] 下

.. rubric:: 源码或pyc 发布的版本

将c9_repair目录 加入到pth 文件

.. rubric:: static/templates发布

将static/templates 使用符号链接(ln -s/mklink), 链接到配置文件STATIC_PATH/TEMPLATE_PATH指定的子目录中

如::

	mklink /D  c:\works\c92\c9\static\js\c9_repair c:\works\c92\c9_repair\static\js\app
	mklink /D c:\works\c92\c9\templates\modules\repair c:\works\c92\c9_repair\templates\repair


python和javascript的猴子补丁
=======================================

如果要修改已有系统的功能,通常的方式就是 继承它,替换它 或直接替换它



