**Java数据库连接(java DataBase Connectivity)**，又称**JDBC**,用于在Java程序中实现数据库操作功能，它提供了执行SQL语句，访问各种数据库的方法，并为各种不同的数据库提供统一的操作接口，java.sql包中包含了JDBC操作数据库的所有类。通过JDBC访问数据库一般有如下步骤：

####	 1. 加载JDBC驱动器及加载JDBC驱动
 在Java程序中，可以通过 `Class.forName(“指定数据库的驱动程序”)` 方式来加载添加到开发环境中的驱动程序，本项目使用的是MySQL数据库，加载MySQL的数据驱动程序的代码为：`Class.forName("com.mysql.jdbc.Driver");`
####	  2. 建立数据库连接，取得Connection对象
 通过DriverManager类创建数据库连接对象Connection。DriverManager类作用于Java程序和JDBC驱动程序之间，用于检查所加载的驱动程序是否可以建立连接，然后通过它的getConnection方法，根据数据库的URL、用户名和密码，创建一个JDBC Connection 对象。如：`Connection connection =  DriverManager.geiConnection(“连接数据库的URL"， "用户名"， "密码”)`。其中，URL=协议名+IP地址(域名)+端口+数据库名称；用户名和密码是指登录数据库时所使用的用户名和密码。
####	  3. 建立Statement对象或PreparedStatement对象
Statement 类的主要是用于执行静态 SQL 语句并返回它所生成结果的对象。通过Connection 对象的 `createStatement()`方法可以创建一个Statement对象：`Statement statament = connection.createStatement()`;
但是Statement对象存在SQL注入漏洞的问题：即SQL可以使用关键字将一条查询语句变成多条，或将后面的语句变成注释【如：or,--】，这个问题可以通过**使用PrepareedStatement(预处理SQL)**来解决：
PrepareStatement继承于Statement，但他与Statement在两方面有所不同：
1）PreparedStatement 实例包含已编译的 SQL 语句。这就是使语句“准备好”。包含于 PreparedStatement 对象中的 SQL 语句可具有一个或多个 IN 参数。IN参数的值在 SQL 语句创建时未被指定。相反的，该语句为每个 IN 参数保留一个问号（“？”）作为占位符。每个问号的值必须在该语句执行之前，通过适当的setXXX 方法来提供。
2）由于 PreparedStatement 对象已预编译过，所以其执行速度要快于 Statement 对象。因此，多次执行的 SQL 语句经常创建为 PreparedStatement 对象，以提高效率。


#### 4. 执行SQL语句
调用Statement对象的相关方法执行相对应的 SQL 语句。
#### 5. 关闭数据库资源
使用完数据库或者不需要访问数据库时，通过Connection和Statement的close() 方法关闭连接和Statement对象。