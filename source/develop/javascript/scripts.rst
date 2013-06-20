一些小脚本
----------------------------------

在线用户数
======================

.. code-block:: javascript

	(function(){
		var online_count = 0;
		iterateTreeNode(workspace.get_chat_window().getComponent('tree').getRootNode(), function(node){ if (node.get('iconCls') ==='online') online_count +=1;})	

		console.log(online_count + 1);	


	})();

	


