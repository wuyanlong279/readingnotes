# mysql基础笔记

1. [连接mysql](#连接mysql)
2. [查询mysql状态](#status)


## <span id="连接mysql">连接mysql<span>
* socet连接
`mysql -S /var/run/mysqld/mysqld.sock -uroot -p`

* ssh连接
`mysql -h127.0.0.1 -P3306 -uroot -p`


## <span id="status">查询mysql状态<span>
* 查询数据库运行状态：`status;`
* 查看当前连接：`show processlist;`
* 查看socket文件所在目录：`show global variables like 'socket';`
