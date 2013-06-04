extjs
---------------------------------------

c9 是我第一次使用extjs 4, 所以,用法还是不断改进中


模式
=========================

我有丰富的桌面编程经验, 但将我的经验结合到extjs还是走了一段弯路. 我目前没有使用extjs的mvc , sencha touch的mvc 我也觉的理解和使用上均不是很方便.

传统的桌面的问题,通常会将后台操作和界面搞在一起,发起一个或多个查询,获得数据,处理数据,显示数据同ui代码混合在一起, 在这种情况下分离关注点很有必要. 但是,基于extjs 的应用, 前后端有物理的分界, 前端代码就是在处理ui, 后端代码就是在查询,分析,处理数据. 如果再在前端使用mvc结构, 无疑是自己找罪受.

组件化, mvc文件结构化在extjs 中比mvc 显得更重要!

组件化

将通用的ui结构 分离到一个组件定义,在使用时仅仅需要使用一个xtype, 比方说 仓库的下拉,部门的下拉框, 商业伙伴的查找框等::

	{xtype: 'local_store_combobox'}, {xtype: 'department_combobox'}, {xtype: 'partner_search_field'}

form/window这些都可以组件化, 通过继承来减少代码

mvc文件结构化

mvc 中最有效的是对文件按功能,类别进行的划分, 但有时一个model几行代码即一个文件, 实在太为过分. 所以,只要对js 文件进行明确的功能划分, 必要时使用多点的文件名来分类, 达到快速定位的效果, 就可以,没有必要遵循mvc的文件结构

约定的

* global.js 全局变量
* base_enum.js 选择项
* models.js extjs model
* windows/control.js 组件, 也可以分离,如 windows.search_field.js
* common.js 公用的
* form_name.js 表单js, form_name用具体的表单名代替,如repair.js/sale_order.js/sale_return.js


通过一个bootstrap.js 区分开发环境和产品环境

在开发环境中加载具体的js文件,在产品环境中只加载合并的js文件


windows forms编程模式

在initComponent中, 将以后需要引用的ui元素变成属性




