#   表操表
##  1.创建表：
```
cerate table  表名{
   列名 列类型，
   ...
}character set 字符集 collate 校验规则 engine 存储引擎；
```
若字符集和校验规则未指定，这以所在数据库的字符集和校验规则为准
```
例：
create table stu{
    id int,
    name varchar(20) comment '用户名'，
    password carchar(32) comment '密码是32位md5值'，
    birthday date comment '生日'
}character set utf8 engine MyISAM;
```
##  2.	查看表结构
```
desc 表名;
```
## 3.	修改表
```
alter table 表名  ADD【添加】/MODIFY【修改】/DROP【删除】
```
#### 3.1	修改表名
```
alter table  原表明 rename  to 新表名
（to可省略）
```
####    3.2	表中插入元素
```
insert into 表名  values(元素1，元素2)
```
####    3.3	表中添加字段
```
alter table 表名  add 字段名 字段类型    
```
## 4.	修改字段名称
```
alter table 表名  change 要修改的字段名  修改后的字段名 数据类型
（新字段需要完整定义，故需要声明字段名+数据类型）
```
## 5.	删除表
```
drop table 表名；
```