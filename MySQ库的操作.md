#   库操作
##  1.创建数据库：
```
create database 数据库名;
指定字符集与校验规则创建数据库：
create database name [指定数据库使用的字符集，[指定数据库使用的校验规则]]
默认使用字符集为：utf8
默认校验规则为:utf8_general_ci
```
例：
```
创建使用utf8字符集的数据库：
create database db  charset = utf8;
创建适用utf字符集，并带校对规则的数据库：
create database db charset=utf8 collate utf8_general_ci;
```
##  2.查看数据库：
```
show databases;
```
### 2.1 显示创建语句
```
show create database 数据库名；
```
##  3.修改数据库：
```
alter database 数据库名;
修改数据库主要是修改其字符集与校验规则：
例：
alter database db charset=gbk;
```
##  4.删除数据库：
```
drop database 数据库名;
```
##  5.备份和恢复：
### 5.1 备份
```
例：
mysqldump -p3360 -u root -p 密码 -B 数据库名 > 数据库备份存储文件路径

mysqldump -p3360 -u root -p123456 -B db >./mytest.sql
```
### 5.2 还原
```
例：
masql> source ./mytest.sql
```
##  6   查看连接状态
```
show processlist;
```