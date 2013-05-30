返修
----------------------------------

返修单
====================================

.. rubric:: 开发者

RepairForm缓存一个对象, 此对象以product_id为key, 称为repair_line_map:

	{
		"1": [RepairLine, RepairLine...],
		"2": [RepairLine, RepairLine...]

	}


当输入明细按钮被点击时::

	var key = String(rec.data.product_id);
	var repair_lines = [];
	if (key in me.repair_line_map){
		repair_lines = me.repair_line_map[key];
	}
	me.input_win.load(repair_lines)

当明细被保存时, 触发一个事件, 更新repair_line_map, 并更新line_grid.store

保存时, 提交repair_lines的所有数据, 在服务端重新生成repair_summary_lines

