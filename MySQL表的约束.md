#   表的约束
字段受数据类型约束，但数据类型约束较单一，需要以下额外的约束，更好地保证数据的合法性，从业务逻辑保证数据的正确性
##  1.空属性
NULL： 空             not null ：非空
![fc5977320ce91d48049cf0606a5f7cc8.png](en-resource://database/780:1)

##  2.默认值
default
![945ad964491542ad7fbfb06069c89d87.png](en-resource://database/782:1)
## 3.列描述
comment ,无实际含义，专门用来描述字段，会根据表创建语句保存
![cd2441e3f7d54f818a7dbe5ad9653073.png](en-resource://database/784:1)

##  4.zerofill格式化输出
```
alter table 表名 change a a int(5) unsigned zerofill;
```
将a字段的内容格式化输出，宽度设定为5时，自动填充0，但数据库中存储的其实还为1
![c74119edd276fb05d36a5dbc4faced86.png](en-resource://database/786:1)
##  5.主键    primary key
用来唯一的约束该字段里面的数据，不能重复，不能为空，一张表最多只能有一个主键，主键所在的列通常为整数类型,**主键对应字段一旦重复将会操作失败**
####    5.1 创建表的时候直接在字段上指定主键
```
create table 表名（
    id int unsigned primary key comment '学号不能为空',
    name varchar(20) not null
）;
```
![f96b2e0f3732d3b0c4c53ff7b0187b37.png](en-resource://database/788:1)
####    5.2 有多个主键时可以使用复合主键
```
create table 表名（
    id int unsigned,
    coures char(10) comment '课程代码'，
    score tinyint unsigned default 60 comment '成绩'，
    primary key(id,coures)  ——id和coures为复合主键
）
```
![39d65b4a1a615f6f879dfff6d8271281.png](en-resource://database/790:1)
复合主键和主键为唯一性不冲突，复合主键相当于将多个主键共同作为一个主键，唯一性是指这个主键里的元素不能重复。
####    5.3 追加主键
```
alter table 表名 add primary key(字段列表)
```
####    5.4 删除主键
```
alter table 表名  drop primary key;
```
![26ff351383c31b20f0d41974c4c93f2a.png](en-resource://database/792:1)
##  6.唯一键     unique
一张表中只能有一个主键，当有多个字段需要唯一性是，使用唯一件来解决
唯一件和主键本质相似，但唯一键可以为空，且可以多个为空，空字段不做唯一性比较
```
create table 表名（
    id char(10) unique comment ''学号，不能重复，但可以为空'，
    name varchar(10)
）;
```
![df93bc6c435bccd5813bac5fba1faef2.png](en-resource://database/794:1)
##  7.外键      
外键用于定义主表和从表之间的关系：外键约束主要定义在从表上，主表则必须是有主键约束或unique约束，当定义外键后，要求外键列数据必须在主表的主键列存在或为null.
```
foreign key  (字段名)  references  主表（列）
```
```
创建主键表：
 create table myclass (

    id int primary key,

    name varchar(30) not null comment'班级名'

);

```
```
创建从表：
 create table stu (

    id int primary key,

    name varchar(30) not null comment '学生名',

    class_id int,

    foreign key (class_id) references myclass(id)

);
```
**foreign key (class_id) references myclass(id)为创建外键**
![6da18146c38120e90691d90449c7562d.png](en-resource://database/796:1)
实现效果：
![05d554a132221eb35597065440c7e8fd.png](en-resource://database/798:1)

##  8.自增长   auto_increment
当对应的字段，不给值，会自动被系统触发，系统会从当前字段中已有的最大值进行+1操作，得到一个新的不同的值，通常与主键搭配使用，作为逻辑主键

* **任何一个字段要做自增长前提是本身是一个索引（key一栏有值）**
* **自增长字段必须是整数**
* **一张表最多只能有一个自增长**
```
create table 表名（
    id int unsigned primary key auto_increment,
    name varchar(10) not null default ' '
）;
```
![6b04d2a7bb90789d8267c2e25a6932df.png](en-resource://database/800:1)
***主键：PRI        唯一键：UNI        外键：MUL***