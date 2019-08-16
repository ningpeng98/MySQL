#   基本查询
##  1.表的增删查改
创建一个新表
```
create table student(
    id int unsigned primary key auto_increment, ——无符号，主键，自增
    sn int not null unique comment '学号',    ——非空，唯一键，解释：学号
    name varcher(20) not null,
    qq varchar(20)
);
```
###    1.1insert 插入
####   1.1.1 单行数据+全列插入
```
insert into students values (100,10000,‘张三’，NULL);
```
####   1.1.2 多行数据+指定列插入
```
insert into students(id,sn,name) values (102,100001,'李四')；  
——仅插入id,sn,name列的数据，qq列的数据为默认值NULL
```
####    1.1.3 插入否则更新  on dupltcate key update
由于主键或唯一键对应的值已经存在会导致插入失败
```
insert into students (id,sn,name) values (100,12223,'王五')；
——id为主键，100值已经存在，主键冲突，插入失败
insert into students (sn,name) values (100001,'赵六')；
——sn为唯一键，100001值已经存在，唯一键冲突，插入失败
```
使用on dupltcate key update：
```
insert into students (id,sn,name) values (100,12223,'王五') on dupltcate key update  id = 999,sn=  888;
——当表中有与要插入数据相同的数据时，执行update，即插入为id= 999，sn = 888;
```
可通过**row_count()函数获取受影响的数据行数**
```
select row_count();
```
####    1.1.4 替换    replace
主键或唯一键若没有冲突则直接插入，若有冲突，则删除原来的插入新的
```
replace into students (id,sn) values (100,'马七')；
```
### 1.2 查找
建一个表：
```
 -- 创建表结构

CREATE TABLE students(

    id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT,     ——主键，自增

    name VARCHAR(20) NOT NULL COMMENT '同学姓名',       ——不为空

    yuwen float DEFAULT 0.0 COMMENT '语文成绩',

    shuxue float DEFAULT 0.0 COMMENT '数学成绩',

    yingyu float DEFAULT 0.0 COMMENT '英语成绩'

);

-- 插入测试数据

INSERT INTO students(name, yuwen, shuxue, yingyu) VALUES

('唐三藏', 67, 98, 56),

('孙悟空', 87, 78, 77),

('猪悟能', 88, 98, 90),

('曹孟德', 82, 84, 67),

('刘玄德', 55, 85, 45),

('孙权', 70, 73, 78),

('宋公明', 75, 65, 30);

Query OK, 7 rows affected (0.00 sec)

Records: 7 Duplicates: 0 Warnings: 0


```
![da5c8dead0f05d624946997470671316.png](en-resource://database/804:1)

####    1.2.1   全列查找
```
select * from students;
```
####    1.2.2   指定列查询
```
select id,sn,name from students;
```
####    1.2.3   查询字段为表达式
```
表达式不包含字段
selece id,name,10  from students;
```
```
表达式包含一个字段
select id,name,yinyu+10 from exam_result;
——将每个人的英语成绩+10再输出
```
```
表达式包含多个字段
select id,name,yuwen+shuxue+yinyu from students;
——将每个人的三门课程成绩加起来输出
```
#### 1.2.4   查询结果重命名 [as]
```
为查询结果重命名
select id,name,yuwen+shuxue+yinyu [as] 总分 from students;
——将每个人的三门课程成绩加起来并命名为总分并输出
```
#### 1.2.5   查询结果去重 distinct
```
查询结果去重
 select distinct shuxue FROM exam_result;
——查询所有人的数学成绩并去掉重复结果后输出

```
### 1.3 where条件
```
查找英语不及格同学
select name,yinyu from students where yinyu<60;
——where 后面为查找条件
 select name, yuwen + shuxue + yingyu 总分 from exam_result

where yuwen + shuxue + yingyu < 200;
——where条件中不能用别名
```

* **常用的条件判断关键字有：**
* **and,or,not:与，或，非**
* **between A and B：在A和B之间，包括A,B，与and可互换使用**
* **in(A,B,C,D):在A，B，C，D这个集合中，与or可互换使用**
* **，like为模糊匹配，%为匹配多个字符，_为匹配严格的一个任意字符**
```
 SELECT name FROM exam_result WHERE name LIKE '孙%';     ——模糊匹配，可找到孙悟空，孙权
 SELECT name FROM exam_result WHERE name LIKE '孙_';     ——精确匹配，只可找到孙权
```
* **=，<=>等于，相对来说前者NULL不安全，NULL=NULL或只要有一边为NULL,的结果都是NULL,后者NULL安全，只有NULL<=>NULL的结果为TRUE即1，其他情况结果都为FALSE即0**
* **!=,<>:不等于**

###    1.4  结果排序    order by
**ASC为升序，DESC为降序，默认为升序ASC**
**NULL比任何值都小，升序时排在最上面，降序时在最下面**
```
select name,shuxue from students order by shuxue;
——升序输出数学成绩
 select name, shuxue, yingyu, yuwen from exam_result

prder by shuxue desc, yingyu, yuwen;
——按数学降序英语和语文升序输出成绩
 select name, yuwen + yingyu + shuxue 总分 from exam_result

order by 总分 desc;
 select name, yuwen + yingyu + shuxue 总分 from exam_result

order by shuxue+yuwen+yinyu desc;
——order by 子句中可以使用表达式和别名
```
###    1.5 筛选查询分页结果 limit
```
select id,name,shuxue,yinyu,yuwen from students order by id limit 3 offset 0;
——将所有人的id,姓名，成绩信息按照id升序输出，当输出格式为从0开始只打印三个
——limit x offset y:x为查询数量，y为起始位置，若结果不足x个，不会有影响
```
### 1.6 更新数据 update...set

```
update students set shuxue = 80 where name = '孙悟空'；
——将孙悟空的数学成绩修改为80分：
 update exam_result set shuxue = shuxue + 30
order by yuwen + shuxue + yingyu limit 3;
——将总分排名后三个的数学成绩+30

```
### 1.7 删除  delete
```
delete from students where name = '孙悟空'；
——删除孙悟空同学的所有数据
delete from students
——删除整张表的数据
```
### 1.8 截断表    truncate 表名
**当你不再需要该表时， 用 drop；当你仍要保留该表，但要删除所有记录时， 用 truncate；当你要删除部分记录时（always with a WHERE clause), 用 delete**
**Truncate是一个能够快速清空资料表内所有资料的SQL语法。并且能针对具有自动递增值的字段，做计数重置归零重新计算的作用。**
* 只能对整表操作，不能像 DELETE 一样针对部分数据操作；
* 实际上 MySQL 不对数据操作，所以比 DELETE 更快
* 会重置 AUTO_INCREMENT 项 
```
truncate students;
```
### 1.9 插入查询结果 insert into 表名 select 

##  2.其他操作
### 2.1 聚合函数
* **count(distinct) expr:返回查询到的*数据数量*，NULL不会计入数量**
* **sum(distinct) expr:返回查询到的数据的*总和*，不是数字没有意义**
* **avg(distinct) expr:返回查询到的数据的*平均值*，不是数字没有意义**
* **max(distinct) expr:返回查询到的数据的*最大值*，不是数字没有意义**
* **min(distinct) expr:返回查询到的数据的*最小值*，不是数字没有意义**
```
select count(qq) from students;
——查询有多少个不为空的qq号
select sun(shuxue) from students;
——统计数学成绩总分
select avg(yuwen+yinyu+shuxue) 平均总分 from students;
——查询平均总分
select max(yinyu) from students where yinyu<70;
——查询英语成绩低于70的最高分
```
### 2.2 group by 子句的使用
在select中使用group by 子句可以对指定列进行分组查询
having针对group by的查询结果进行筛选，where关键字无法用于group by 语句中，用having可以实现