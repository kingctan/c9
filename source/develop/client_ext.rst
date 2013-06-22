客户端扩展
----------------------------

与 :doc:`ext` 相比,　这里的客户端扩展专指通过c9 界面进行,主要使用javascript, 调用预定义的功能完成,　如果不存在可调用的功能.　还是需要通过 :doc:`ext` 来完成

客户端扩展将支持

* job
* form - 窗体/表单
* query - 查询
* report - 报表

当前,　c9 仅支持 job功能, 你可以在应用程序对象树 Jobs 中定义,删除,编辑,运行job

.. image:: /images/job.png
	:width: 640
	:height: 480

使用客户端扩展除了需要javascript知识外，还需要了解extjs. 扩展将通过extjs 创建ui, 访问数据。



job 
=============================

job 是一段javascript  脚本， 注意c9 最终会如下运行

.. code-block:: javascript

	(function(){
		//你的job脚本

	})();


所以，没有必要将你的脚本包裹在(function(){})()块中


job可以在job界面中运行，也可以通过菜单项暴露， 从而指定给菜单调用， 当指定给菜单项时， uri 用 /jobs/job_name 的格式

通过菜单项/菜单管理的job , c9会自动创建一个tab_菜单名的父panel, 你的代码应该是这样的

.. code-block:: javascript

	
	parent_panel.add(你自己的panel); //parent_panel自动提供

如果不借助于c9的体系,自行添加到workspace.tabs,需要使用不同的代码

.. code-block:: javascript

	var closable = true;
	var id = 'tab_job_test';
	// var t = tabs.getComponent(id);
	// if (t) {
	//   tabs.setActiveTab(t, closable);
		
	// } else{
		
	// 	main();
	// }	
	function main(){
		// var panel = workspace.tabs.add({
		// 	title: '部门',
		// 	iconCls: 'application_form',
		// 	itemId: id,
		// 	closable: true,
		// 	layout: 'fit',
		// 	items: [grid]
			
		// 	});
		
		
		// workspace.tabs.setActiveTab(panel);


	}

	
startup job
=============================

如果你将job命名为startup， 则在系统启动时, c9会自动调用该脚本。 开发者可以在这些脚本中针对所有用户或特定用户执行该脚本，通常用于自定义工具条/导航挂接功能。

.. code-block:: javascript

	console.log('hello, all');

	if (workspace.user.name === 'jjx') {
		console.log('hello, jjx');
		
	}

workspace
=================================

未来, 大部分全局变量均将集中到一个 workspace 变量中，你可以通过workspace变量引用大部分c9 元素. 抱歉，现在还存在两种命名形式

.. rubric:: 界面类

* statusBar - 状态条 Ext.toolbar.Toolbar 
* toolbar - 工具条, Ext.toolbar.Toolbar
* tabs - Ext.tab.Panel
* accordion - Ext.panel.Panel
* get_chat_window() - 获得聊天窗口

.. rubric::  配置

通过 workspace.config访问

* START_MONTH
* TOOLBAR_MODULES
* FORM_NEW_REC_MAP
* FORM_CLASS_MAP
* RESOURCE_MAP
* use_chat
* get_resource(model)

.. rubric:: 其他

* user - 当前用户
* form_holder - 该变量持有单例的表单实例, 你可以使用form_holder.表单名访问表单对象，如果已经存在, 如form_holder.sale_order/form_hodler.purchase_order
* open_form(form_name, form_id)  打开一个指定的表单(singleton)
* new_form(form_name)  打开一个新建表单
* open_new_form(form_name, form_id)  打开一个表单(非singleton, 每次都是一个新实例)


.. code-block:: javascript

	workspace.open_form('allot', 1000); // 打开一个id 为1000的调拨单
	form_holder.allot; // 访问当前的调拨单 表单实例
	workspace.open_form('allot', 1000) === form_holder.allot; //open_form是singleton的,所以是true


表单有一定的范式, 如
* form 如果存在一个form
* form2 如果存在第二个form
* form_tab 当存在多个form时 用form_tab组织两个form
* line_tab 组织line_grid和action_grid
* line_grid 明细行
* line_gird2 如果存在第二个明细行
* action_grid 表单活动行
* workflow 工作流面板 C9.workflow.ExecutePanel 实例


workspace.tabs
===================

c9 用一个Ext.tab.Panel来放置多个同时打开的功能, 你可以通过 workspace.tabs来访问已经打开的界面并进行定制

.. code-block:: javascript

	workspace.tabs.getComponent('tab_菜单名'); // 菜单名可查询aot - 菜单功能

	//或通过worksapce.tabs.items 访问
	workspace.tabs.items.each(function(p){
		console.log( p.getItemId());
	});
	
	//tab_workflow_current_action
	//tab_user
	//tab_role
	//tab_workflow



一般 , 获得的是一个标准的Ext.panel.Panel, 你可以按extjs常识继续访问


workspace.showNode
=================================

如果你已经知道一个定义, 你可以直接调用workspace.showNode 而不是通过左侧导航来打开它. showNode需要传递一个node和是否允许关闭按钮的参数, 你可以这样试试

.. code-block:: javascript

	workspace.showNode(workspace.profie_node); // 或 workspace.showProfile() 打开个性化设置功能
	workspace.showNode(workspace.borad_node); // 或workspace.showBorad();
	workspace.showWorkbench(); //显示工作台

	// node 范例
	workspace.showWorkbench = function() {
		workspace.showNode({
			name: 'workflow_current_action',
			text: '工作台',
			iconCls: 'house',
			icon_cls: 'house',
			src: '/modules/workflow_current_action'
		});
	}


showNode遵循存在则活动该tab,不存在则创建的规则.

model/store
===========================

数据访问主要通过model或store访问,查看 c9提供的model列表