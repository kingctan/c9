笔记
----------------------------

搜索表达式
==========================

c9 允许从客户端发起查询， 可以使用model__field__查询条件，其中model__部分通常不使用，一般就是field__查询条件, 如name__contains, 如果需要通过or查询多个字段, 可使用如下模式 name__contains__or__ad_name__contains__or__help_code__contains

缓存
============================

在登录时,用户会在本地保存一个APPLICATION_CACHE对象, 每个属性为一个对象

* bank {"1": 'bank1', "2": 'bank2'}


APPLICATION_CACHE主要用于lookup查找,将数字id值替换为文本值, 由于启用了cache, APPLICATION_CACHE即使再次登录也不一定会更新, 他当然也无法获取他的改变. 为了减低对用户的干扰,当前临时的一个措施时在维护基础数据更新时同时更新APPLICATION_CACHE, 建议调用(baseenum.js)

    function update_application_cache(key, id, value){
    	APPLICATION_CACHE[key][String(id)] = value;

    }



结转步骤
======================

1. 停止服务
2. 备份当前数据
3. 恢复到一个新的数据库，如 c92012
4. 将数据写入历史条码库 report/barcode_history.py
5. 执行脚本 scripts/carry_over.py
6. 执行脚本 scripts/profit_over.py 将利润结转到322利润分配科目，再清除5开头的科目值
7. 还原数据库，进行vacuumdb -a -U postgres /reindexdb -a -U postgres