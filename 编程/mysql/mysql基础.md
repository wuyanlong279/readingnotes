# mysql基础笔记

1. [连接mysql](#连接mysql)
2. [查询mysql状态](#查询mysql状态)
3. [sql语言](#sql语言)
4. [mysql数据类型](#mysql数据类型)
5. [mysql数据对象](#mysql数据对象)

## <span id="连接mysql">连接mysql<span>
* socet连接
`mysql -S /var/run/mysqld/mysqld.sock -uroot -p`

* ssh连接
`mysql -h127.0.0.1 -P3306 -uroot -p`


## <span id="查询mysql状态">查询mysql状态<span>
* 查询数据库运行状态:`status;`
* 查看当前连接:`show processlist;`
* 查看socket文件所在目录:`show global variables like 'socket';`
* 查看数据库database:`show databases;`
* 查看databas中表:`show tables;`


## <span id="sql语言">sql语言<span>
### sql语句分类
* DDL数据定义:创建表，修改表
 - 创建DATABASE:`CREATE DATABASE database_name;`
 - 使用DATABASE:`use database_name;`
 - 创建数据表:
 ```
 CREATE TABLE table_name(
   id int(10),
   name varchar(20),
   age int(10),
   #设置主键
   PRIMARY KEY(id)
   );
 ```
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


## <span id="mysql数据类型">mysql数据类型<span>
* 数字类型:
  - 整形:
    - TINYINT:占1字节
    - SMALLINT:占2字节
    - MEDIUMINT:占3字节
    - INT:占4字节(int(11)与int(21)储存空间和范围完全一样,区别在于前面补0为多少位)
    - BIGINT:占8字节
  - 浮点型:
    - FLOAT:4字节,单精度
    - DOUBLE:8字节,双精度
    - DECIMAL(定点数):根据存储内容占用字节,高精度
      DECIMAL(M,N):M代表总精度,N代表小数点位数(1<M<254,0<N<60)


* 文本类型:
  - char:存储定长,如char(10),存储man占用10字节
  - varchar:存储边长,如varchar(10),存储man占用4字节,首个字节为长度
  - text:大多为存储溢出页,效率低,不建议使用


* 时间类型:
  - DATE:3字节,存储年月日,如2015-01-01
  - TIME:3字节,存储时分秒,如11:11:11
  - TIMESTAMP:4字节,存储年月日时分秒,**根据时区转换**,范围(1970-01-01 00:00:01——2038-01-19 03:14:07)
  - DATETIME:8字节,存储年月日时分秒,范围(1000-01-01 00:00:01——9999-12-31 23:59:59)
  - BIGINT也可以储存时间,存储Unix时间戳


## <span id="mysql数据对象">mysql数据对象<span>
* DATABASE/SCHEMA:  
mysql中database与schema一样  
一个database包含一张或多张表,一张表包含一个或多个字段,一张表包含一条或多条记录,一张表包含一个或多个索引  
多个database用途为业务或资源的隔离


* INDEX索引:
  - 创建索引:`CREATE INDEX index_name table_name col_name(字段名) [ASC/DESE] (排序) index_type(索引类别);`
  - 插入索引:`ALTER TABLE ...`
  - 约束:
    - 唯一约束:UNIQUE KEY `ALTER TABLE 'table_name' ADD UNIQUE KEY unique_name(useid);`
    - 主键:PRIMARY KEY `ALTER TABLE 'table_name' ADD PRIMARY KEY(id);`,主键也是一种唯一约束
    - 外建约束: `ALTER TABLE 'table_name' ADD CONSTRAINT(约束)  constraint_name FOREIGN KEY(useid) REFERENCES 'table_name(外建表名)'(useid); `
    - **注意事项**:
      - 必须是INNDDB表
      - 相互约束的字段类型必须一样
      - 主表约束字段必须有索引
      - 约束名称必须唯一,即使不在一张表上


* VIEW视图:
  - 作用:
    - 视图将一组查询语句构成结果集,是一种虚拟结构,并不是实际数据
    - 视图能简化数据库的访问,能将多个查询语句结构化为一个虚拟结构
    - 视图可以隐藏数据库端的表结构,提高数据库的安全性
    - 视图也是一种权限管理,只对用户提供部分数据
  - 创建视图: `CREATE VIEW view_name AS select * from table_name(视图中包含的查询逻辑);`


* TRIGGER触发器:在数据写入数据表之前或之后做一些其他动作


* FUNCTION函数:


* PROCEDURE存储过程:
