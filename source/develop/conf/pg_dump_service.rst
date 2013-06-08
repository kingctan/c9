postgresql 自动备份服务
--------------------------------------------------

例子::

	{
	    "INTERVAL": 1200,
	    "BACKUP_PATH": "/home/jiang/backup",
	    "PG_DUMP": "/usr/lib/postgresql/9.2/bin/pg_dump",
	    "ZIP": "7z",
	    "ZIP_PASSWORD": "7z压缩密码",
	    "DATABASE": "c9",
	    "PASSWORD": "数据库口令",
	    "BACKUP_TIME": [
	        {
	            "hour": 20,
	            "minute": 0
	        },
	        {
	            "hour": 6,
	            "minute": 0
	        }
	    ]

	}

配置项
=======================================

* INTERVAL 检查间隔
* BACKUP_PATH 备份到那里,绝对路径
* PG_DUMP  pg_dump/pg_dump.exe 文件全路径
* ZIP  7z/7z.exe 文件全路径
* ZIP_PASSWORD  压缩文件密码
* DATABASE 备份那个数据库
* PASSWORD 数据库口令
* BACKUP_TIME 列表, 每个项由hour/minute组成,表示几点几分备份一次

