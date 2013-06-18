笔记
----------------------------

搜索表达式
==========================

c9 允许从客户端发起查询， 可以使用model__field__查询条件，其中model__部分通常不使用，一般就是field__查询条件, 如name__contains, 如果需要通过or查询多个字段, 可使用如下模式 name__contains__or__ad_name__contains__or__help_code__contains

如果url中出现了类似/api/users?approve=&name__contains__or__help_code_contains的请求，对于approve的处理是个难题，不需要进行approve的查询或是approve为False, 这里, c9使用第一种的理解，忽略该参数.

表达列表

1. eq  等于
2. neq 不等于
3. isnull  is null
4. nisnull is not null
5. blank 等于空白
6. nblank 不等于blank
7. gt 大于
8. gte 大于等于
9. lt 小于
10. lte 小于等于
11. contains 包含
12. startswith 开始于
13. endswith 结束于

缓存
============================

在登录时,用户会在本地保存一个APPLICATION_CACHE对象, 每个属性为一个对象

* bank {"1": 'bank1', "2": 'bank2'}


APPLICATION_CACHE主要用于lookup查找,将数字id值替换为文本值, 由于启用了cache, APPLICATION_CACHE即使再次登录也不一定会更新, 他当然也无法获取他的改变. 为了减低对用户的干扰,当前临时的一个措施时在维护基础数据更新时同时更新APPLICATION_CACHE, 建议调用(baseenum.js)

    function update_application_cache(key, id, value){
    	APPLICATION_CACHE[key][String(id)] = value;

    }


基础信息缓存问题汇总
==================================

无 指除了说明的, 没有缓存问题

通常存在两种问题,一是指定窗口打开后相关数据发生变化, 如 8 , 需要关闭该窗口重新打开反映变化, 此理论不属于问题

第二种程序是程序处理的,一种是程序从本地缓存中获取数据, 如员工下拉框, 仓库下拉框等,  在没有刷新缓存时这个数据不会变化, 其次是只加载一次, 以后不在重复加载, 如部门下拉框.

由于C9对所有的单据窗体使用单实例方式, 像销售单窗体只创建一次, 所以加剧缓存问题

前一种解决方法, 刷新应用程序缓存, 必要时关闭当前窗口, 后一种解决方法,刷新整个应用

但对于用户而言, 操作造成很大的困扰, 所以,最好用统一的方法解决此问题 todo 

如果不涉及单据, 在基础数据部分,缓存的问题可能性如下

1. 用户 ,员工下拉框 local_employee_combobox 随登录时缓存, 刷新缓存有用
2. 角色 无
3. 工作流 无
4. 地区 无 如果对用户授权, 新赠的用户可能看不到 , 需要在用户中为自己授权, todo 是否在新增时完成给自己授权这个动作
5. 商业伙伴 左侧的地区需要关闭商业伙伴窗口,重新打开, 其他无
6. 品牌 无
7. 货品类型 无
8. 产品信息 左侧货品类型自窗口打开后如改变需要关闭 产品信息 窗口反映变化,其他 无
9. 仓库 无
10. 货币 无
11. 账户无, 检查引用 如未做单 期初账户输入否 , 新增的账户可能看不到,同地区
12. 科目 无
13. 部门 新增的部门可能看不到,同地区
14. 员工类型 无
15. 员工 部门/员工类型需要关闭员工窗口反应变化,其他employee_type_combobox/department_combobox 窗体中的部门只加载一次,需要刷新应用 todo 需要处理
16. 收入支出 无
17. 核算类型 无



结转步骤
======================

1. 停止服务
2. 备份当前数据
3. 恢复到一个新的数据库，如 c92012
4. 将数据写入历史条码库 report/barcode_history.py
5. 执行脚本 scripts/carry_over.py
6. 执行脚本 scripts/profit_over.py 将利润结转到322利润分配科目，再清除5开头的科目值
7. 还原数据库，进行vacuumdb -a -U postgres /reindexdb -a -U postgres