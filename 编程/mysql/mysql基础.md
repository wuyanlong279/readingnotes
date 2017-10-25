# mysql基础笔记

1. [连接mysql](#连接mysql)
2. [查询mysql状态](#status)
3. [sql语言](#sql语言)

## <span id="连接mysql">连接mysql<span>
* socet连接
`mysql -S /var/run/mysqld/mysqld.sock -uroot -p`

* ssh连接
`mysql -h127.0.0.1 -P3306 -uroot -p`


## <span id="status">查询mysql状态<span>
* 查询数据库运行状态:`status;`
* 查看当前连接:`show processlist;`
* 查看socket文件所在目录:`show global variables like 'socket';`
* 查看数据库database:‘show databases;’
* 查看databas中表:'show tables;'


## <span id="sql语言">sql语言<span>
### sql语句分类
* DDL数据定义:创建表，修改表
 - 创建DATABASE:`CREATE DATABASE database_name;`
 - 使用DATABASE:`use database_name;`
 - 创建数据表:
 `CREATE TABLE table_name(
   id int(10),  
   name varchar(20),  
   age int(10),  
   #设置主键  
   PRIMARY KEY(id)
   );`
  - 修改数据表:
   - 增加一个字段:`ALTER TABLE table_name ADD COLUMN aa int(10);`
   - 修改一个字段:`ALTER TABLE table_name MODIFY COLUMN aa int(20);`
   - 删除一个字段:`ALTER TABLE table_name DROP COLUMN aa;`
  - 删除数据表:`DROP TABLE table_name;`


* DML数据操作:数据表中的增删改
  - 插入记录:`INSERT INTO table_name(id,name,age) VALUES(1.'aa',22);`
  - 更新记录:`UPDATE table_name SET age=29 WHERE id=1;`
  - 删除记录:`DELETE FROM table_name WHERE id=1;`


* select:查询记录
  - 查询表中记录:`SELECT * FROM table_name WHERE id=1;`


* DCL权限管理:控制数据库访问权限设置
  - GRANT
  - REVOKE


* TCL事务控制:控制事务进展
  - COMMIT提交事务
  - ROLLBACK回滚事务

  
