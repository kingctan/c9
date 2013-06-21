c9 运行状态检查
--------------------------------

1. 首先查看nginx 的错误日志，通常它的目录是 c9[版本号]/nginx-1.4.1/logs/error.log , 如果出现upstream error , 表示c9 的tornado 后端down机. 其它错误均不影响正常访问

2. c9 现在已经交付一个叫 servicemonitor的 服务状态监控程序， 它隔80秒会依次访问 c9的 tornado web 后端, 检测 nginx -> tornado -> proxy -> application server -> proxy -> tornado ->nginx 的通路。 如果在40秒内某个后端没有返回，则它会自动重启该后端。 可以查看 c9[版本号]/logs/servicemonitor.log 

自6月16日 在DELETE请求中错误的关闭zmq上下文 bug修正后， 1 应该不会发生，而 2 也就没有起作用了，但也可以通过 servicemonitor.log 查看本地的访问情况::

	2013-06-21 16:01:15+0800 [-] Starting factory <HTTPClientFactory: http://localhost:8000/api/heart>
	2013-06-21 16:01:15+0800 [-] Starting factory <HTTPClientFactory: http://localhost:8001/api/heart>
	2013-06-21 16:01:15+0800 [-] Starting factory <HTTPClientFactory: http://localhost:8002/api/heart>
	2013-06-21 16:01:15+0800 [-] Starting factory <HTTPClientFactory: http://localhost:8003/api/heart>
	2013-06-21 16:01:15+0800 [-] Starting factory <HTTPClientFactory: http://localhost:8004/api/heart>
	2013-06-21 16:01:15+0800 [-] Starting factory <HTTPClientFactory: http://localhost:8005/api/heart>
	2013-06-21 16:01:15+0800 [HTTPPageGetter,client] Stopping factory <HTTPClientFactory: http://localhost:8005/api/heart>
	2013-06-21 16:01:15+0800 [HTTPPageGetter,client] Stopping factory <HTTPClientFactory: http://localhost:8001/api/heart>
	2013-06-21 16:01:15+0800 [HTTPPageGetter,client] Stopping factory <HTTPClientFactory: http://localhost:8003/api/heart>
	2013-06-21 16:01:15+0800 [HTTPPageGetter,client] Stopping factory <HTTPClientFactory: http://localhost:8000/api/heart>
	2013-06-21 16:01:15+0800 [HTTPPageGetter,client] Stopping factory <HTTPClientFactory: http://localhost:8004/api/heart>
	2013-06-21 16:01:15+0800 [HTTPPageGetter,client] Stopping factory <HTTPClientFactory: http://localhost:8002/api/heart>

可以对比每个后端starting/stopping的时间来检查服务状态是否良好。如果starting/stopping超过秒，通常表明当时 application server 吃紧，如果持续如此，可能需要增多application server进程。如果是超过40秒，则你会在servicemonitor.log看到 c9[版本号]webserver[进程数] 服务停止和重启的信息。


3. windows 任务管理器

通过观察windows 任务管理器，可以大约了解当前访问状态，并推断是否需要增加 application server进程

在windows 任务管理器中， 按 内存 占用排序

* 占用100M以上的pythonw进程通常就是application server , 在不同的机器上可能有不同数量的进程，如4个或是12~13个. 内存占用通常固定在120m只能
* 占用40M 左右的pythonw进程通常就是tornado 后端， 在不同的机器上可能有不同数量的进程，如4个或6个。 内存占用通常固定在40M左右
* 正常情况下只有application server进程的cpu占用有参考价值
* 理想的情况下，在一定的时间段内，最好有1个或以上aplication server进程空闲(cpu为零)，如果长时间所有application server 进程均被占用( cpu 不为零) , 可以适当增加application server 进程(视cpu/内存的空闲情况而定). 这个一定的时间段长度应该根据实际情况访问状态而定, 在访问高峰时，可能会有短暂的所有进程均被占用的情况, 应该可以被视为可以接受，无需调整进程。
* 如果有大量application server 进程空闲( cpu 为零), 则说明当前访问空闲。 所有application server进程均为0，说明当前没有访问
* 如果在较短时间内，如1-5秒内总有1个或以上application server进程空闲( cpu为零)，说明当前进程设定完全能满足需要


在linux 可以通过top命令查看


4. 如何判断下载速度

使用chrome, 在访问c9前先按下 f12, 然后点击network, 点击XHR , 然后访问c9, 登录，通过查看/api/cache的查看size和time(有两行,需要看上面行的数字) 就可以知道下载量和用时的比例，从而判断下载速度。一般size 都在150kb之内, time通常应该在2秒左右。(其它项通常由于下载量太小，无法成为判断依据)

也可以清除浏览器缓存， f12-> network -> scripts, 然后访问c9, 查看 ext-all.js?_dc=版本号 文件的下载情况. ext-all.js只通过nginx，不经过c9系统。