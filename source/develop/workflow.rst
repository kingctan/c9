工作流
------------------------------


体系结构
====================================

C9的工作流由以下概念组成

* 工作流定义
* 工作流实例, 每个创建的工作流均有一份工作流定义的副本
* 当前活动 , 当前需要执行的工作流活动
* 工作流活动备份



工作流定义
====================

一个工作流有一些Step组成, Step可以是简单的, 也可以是 JoinStep/MultiChoiceStep/ParallelStep


.. rubric:: Step的completed和set_completed

调用 completed 是执行一个流程动作, 并非是完成该动作, 动作是否完成取决于step的类型,如果是简单的步骤,则调用该方法该步骤即完成,如果是多选一,则需要有一个子步骤为True, 如果是会签和并行,则需要所有子步骤为True

set_completed 执行表示改动作已经完成

在执行流程动作时,前端界面总是提交id和child_ids, 前者是要执行的动作,后者是需要同时执行的该动作的子动作, 在处理时系统中是先处理child_ids , 这样在step的completed中,实际上没有判断自身是否是子step的操作.当然,这样处理方式,当前代码只运行传递两级动作. 但对于进销存而言,应该是够了

查看工作流的代码, 可以看到每个大的步骤, 最多允许三级, 在实际中,通常只用到二级



不足
=========================

* 工作流依赖事务, 在工作流中,不要有session.commit这样的操作
* 当获得一个workflow_current_action 时,没有办法立即知道要做什么, 必须重建workflow,然后获取步骤才行, 理论上,你不completed这个动作,你就不知道这个动作是否是真的结束. 但completed会调用set_completed, 从而进行数据库操作
* WorkflowBase 预建的execute/audit方法 事先已经有db操作
.. code-block:: python

    step = workflow.get_step_by_id(id)

