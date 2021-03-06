
销售单
-------------------------

属性
=====================
常规

* 编码 - 自动生成
* 创建日期 - 自动生成, 当单据被执行时,创建日期会自动修改为执行日期
* 发票类型 
* 仓库
* 商业伙伴
* 员工 - 默认为登录账号绑定的员工
* 部门 - 默认为登录账号绑定的员工所属部门
* 总金额 - 自动生成
* 送货地址  - 选择商业伙伴时自动生成
* 备注

其它

* 账期 - 选择商业伙伴时自动生成
* 联系人 - 选择商业伙伴时自动生成
* 联系电话 - 选择商业伙伴时自动生成

订单明细

* 货品 - 选择货品时自动生成
* 数量 - 必须输入
* 单价 - 可以为0
* 当前限价 - 如果为该客户设定了价格体系并且该产品设置了价格(参考售价a/b/c), 则这里会显示该客户该产品的当前限价,如果小于该限价,系统会用颜色区分
* 合计金额 - 自动生成
* 备注 
* 详细 - 点击该图标 会显示该产品的库存,成本等信息



新建销售单
=====================

1. 从工具栏点击销售-销售单或从导航中选择销售-销售单 - 新建
2. 输入销售单属性
3. 输入销售明细,参考下方说明
4. 点击保存

.. rubric:: 合作伙伴输入

1. 在文本框中输入合作伙伴名称或拼音(名称拼音的首字母,必须大写), 回车

2. 在弹出的对话中选择客户,双击确认



销售明细输入
===================

通常 将光标停留在 名称/拼音框, 你可以输入

* 产品名称的部分
* 产品名称的拼音首字母缩写, 当前,必须大写

然后按回车或点击新增明细图标

选择货品窗口是左右(上下),结构,顶部的输入框允许你更换搜索关键字, 左边是货品类别,如果*选择货品类型根节点表示在全部货品类型中搜索,而选择任意一个货品类型则表示在该货品类型及子类别中搜索*

右边的上面是产品列表, 注意如果你已经选择了仓库,则当前库存和在途库存显示该仓库的当前库存和在途库存数量

右边的下方是*所有仓库*(没错,是所有仓库,这里没有过滤权限?是否需要?) 该货品的当前库存和在途库存数量

你可以选择一行,双击回到销售单输入界面,如果要选择多个记录,先核选该行前的输入框, 然后点击多选输入按钮

如果需要移除明细行,将光标定位到该行,然后点击删除明细图标

编辑记录,只需要将光标定位到该行,然后输入内容, 用回车或点击 更新即可, 按esc一次或点击cancel按钮可以取消修改


确认销售单
=====================

1. 双击打开销售单
2. 在表单工具栏点击确认, 你可以在确认按钮旁的输入框输入本次确认的说明,如钱已经到账,此说明会显示在该单据活动中

当你确认销售单后,该销售单将进入工作流程

审核/退回销售单
========================

1. 从我的单据双击销售单打开销售单(如果你对该销售单有审核权限)或
2. 从我的工作流中选择要审核的销售单,双击打开
3. 在右边下方的审核/退回中选择审核或退回,输入审核说明(非必须), 点击确认

修改销售单
===================

在单据尚未执行前,你均可以修改销售单(仅限本人), 流程操作者只能退回

你可以修改销售单,然后点击保存,此时,销售单状态会变成草稿,你需要重新确认,将单据重新放入流程中

执行/退回销售单
========================

1. 从我的单据双击销售单打开销售单(如果你对该销售单有执行权限)或
2. 从我的工作流中选择要执行的销售单,双击打开
3. 在右边下方的执行/退回中选择执行或退回,输入执行说明(非必须), 点击确认


执行通常会因为 库存不足 而失败,当前c9 不允许负库存, 所以,解决的方法是先采购或调拨,保证库存的前提下继续执行该销售单


打印销售单
======================

只要销售单已经创建, 则就可以打印该销售单

1. 打开需要打印的销售单,然后在工具栏中选择打印
2. 出现打印窗口, 在该窗口右下方的图标栏中选择打印图标(如果不显示,将鼠标光标移动到该窗口的右下方位置)
3. 在弹出的对话框中点击打印按钮

.. rubric:: 关于打印模板

由于不同业务需要, c9预先创建了一些模板

* 默认模板不显示单价和金额
* cway 模板显示单价和金额
* fire 模板打印条码,不显示单价和金额
* fire_with_price 打印条码,显示单价和金额

设置打印模板的过程如下

1. 在C9 工具栏中选择个性化设置
2. 保存缺省模板路径为空则为缺省,否则可输入cway/fire/fire_with_price其中之一的值,点击保存

当前,默认的纸张大小为 宽 21 cm/高9.2cm


.. rubric:: 开发者

模板的路径为 TEMPLATE_PATH/pdf (TEMPLATE_PATH参考配置文件)

