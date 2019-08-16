#   MySOL内置函数
##  日期函数
*   当前日期：current_date()
*   当前时间：current_time()
*   当前时间戳：current_timestamp()
*   返回datetime参数的日期部分：date(datetime)
*   在date中添加日期或时间：date_add(date,interval d_value_type)
    d_value_type可以为：year,minute,second,day
*   在date中减去、日期或时间：date_add(date,subl d_value_type)
    d_value_type可以为：year,minute,second,day
*   两个日期的差：datediff(date1,date2)——单位为天
*   当前日期时间：now()
### 实例
```
select current_date();
获取年月日；
 select current_time();
获取时分秒
select current_timestamp();
获取时间戳 
 select date_add('2017-10-28', interval 10 day);
在指定日期基础上+10天
select date_add(current_timestamp(), interval 2 year);
自动获取时间戳并在此基础上-2年
 select datediff('2017-10-10', '2016-9-1');
 计算两个日期差
```
##  字符串函数
*   返回字符串字符集：charset(str);
*   连接字符串：concat(string2 [,...]);
*   返回substring 在string中出现的位置，没有返回0：instr(string,substring);
*   字符串转换成大写/小写：ucase(string)/lcase(string)
*   从string中左边起取length个字符：left(string,length)
*   string的长度：length(string)
*   在str中用strB替换strA:replace(str,strA,strB)
*   逐字符比较两个字符串的大小：strcmp(string1,string2)
*   从str的index开始，取lengrh个字符：substring(str,index,length);
*   去除前空格或后空格：ltrim(string)  rtrim(string)  trim(string)
### 实例
![cb2e15637c930ccc4da68ecb555b63d6.png](en-resource://database/812:1)
![a44b98c919c8dcfe20d45d90162651ff.png](en-resource://database/814:1)
##  数学函数
*   绝对值：abs(num)
*   向上去整/向下去整：ceiling(num)/floor(num)
*   格式化，保留小数位数：format(num,保留小数的位数)
*   取模，求余数：mod(num,denominator)
*   返回随机浮点数：rand()
### 实例：
```
select rand();
产生随机数
```
![a07e1409118d1dd074f975191b2ed503.png](en-resource://database/816:1)
##  其他函数：
查询当前用户：select uesr();
显示正在使用的数据库：select database();
判断:select ifnull(val1,val2);——如果val为null,返回null2否则返回null1的值
### 实例：
![68c644efb26103a872b686dc9f25f4d0.png](en-resource://database/818:1)