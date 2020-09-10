#### Mac 安装Navicate Premium
    Mac安装Navicate Premium 提示：“文件已损坏，请将文件移动至垃圾箱” 解决方法：
    1.打开终端：sudo bash
    2.进入root用户下执行：xattr -cr /Applications/Navicat\ Premium.app/
    3.重启Navicate。
    注：/Applications/Navicat\ Premium.app/ 是应用安装后的路径 ， Mac 应用安装后一般都在 /Applications/ 下有***.app 文件，也就是应用的入口文件。

登陆
```
mysql -u用户名 -p密码
```
切换数据库:
```
use databaseName
```
展示数据库中所有表：
```
show tables；
```

查看数据库表字段:
```
desc 表名
```

修改表中所有字段的字符集：
```
ALTER TABLE 表名 CONVERT TO CHARACTER SET utf8
```
修改表名称
```
ALTER  TABLE table_name RENAME TO new_table_name
```
修改主键
```
ALTER TABLE t_sys_user DROP PRIMARY KEY ,ADD PRIMARY KEY ( `id` );
```
查看表索引：
```
show index from tblname
```
修改字段类型：
```
alter table 表名 modify column 字段名字 decimal(18, 4) ;
```
添加更新时间和创建时间字段
```
ALTER TABLE TableName 
ADD COLUMN create_time timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP, 
ADD COLUMN update_time timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP AFTER create_time;
```
添加索引（一般将索引添加在频繁查询的字段上） 格式：
```
ALTER TABLE 表名 ADD 索引类型 （unique,primary key,fulltext,index）[索引名]（字段名）

(1) alter table table_name add index index_name (column_list) ;

(2) alter table table_name add unique (column_list) ;

(3) alter table table_name add primary key (column_list) ;
```
删除索引：
```
drop index index_name on table_name
```
删除数据库表字段
```
alter table table_name  drop column colume_name1,drop column colume_name2;
```
#### Mysql不同索引的区别
    mysql索引的数据结构：B-Tree，是一种多路平衡二叉树的结构，每次查询都是从根节点root开始，遍历子节点。
    1.普通索引：最基本的索引，没有任何限制。
    2.唯一索引：和普通索引类似，但是唯一索引的列值必须唯一，但允许有空值。
    3.主键索引：特殊的唯一索引，不允许有空值。
    4.组合索引：为了进一步提高mysql效率，遵循“最左前缀”原则。创建符合索引时应将最常用（频率）做限制条件放在最左边，依次递减。
    5:全文索引：仅可用于 MyISAM 表，针对较大的数据，生成全文索引很耗时耗空间。

#### 数据库设计三范式：
    第一范式：列不可再分。
    第二范式：每个表只描述一件事。
    第三范式：不存在对非主键列的传递依赖。
#### mysql事物四个属性：
    1.原子性：要么全执行，要么全不执行。（非黑即白）
    2.一致性：当事务完成时，数据必须处于一致状态，
    3.隔离性：并发的事务彼此隔离，相互独立，不能影响或依赖其他事务
    4.永久性：事务完成后，对数据库的操作永久保持。

#### 存储过程优化思路：
    1.尽量利用sql语句来替换一些小循环。例如：聚合函数，求平均值。
    2.中间结果存放于临时表，加索引。
    3.少使用游标。游标（只读，不可滚动，敏感。不可以通过游标修改更新数据，不能跳）

#### 开启远程访问权限
    use mysql;
    update user set host = '%' where user = 'root'; (使mysql root用户可以连接上任意的ip地址)
    FLUSH PRIVILEGES

#### 临时修改mysql的严格模式，将严格模式取消
    use mysql;
    set sql_mode=(select replace(@@sql_mode,'ONLY_FULL_GROUP_BY,',''));     
    set @@global.sql_mode=(select replace(@@global.sql_mode,'ONLY_FULL_GROUP_BY,','')); 































