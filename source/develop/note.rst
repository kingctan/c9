笔记
----------------------------

搜索表达式
==========================

c9 允许从客户端发起查询， 可以使用model__field__查询条件，其中model__部分通常不使用，一般就是field__查询条件, 如name__contains, 如果需要通过or查询多个字段, 可使用如下模式 name__contains__or__ad_name__contains__or__help_code__contains