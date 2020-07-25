### 3.1 SQL通用语法注释

```
-- 单行注释【这个必须有空格】

# 单行注释【这个可以没有空格】

/* 多行注释 */	
```

#### 3.3.1 操作数据库

##### 3.3.1.1 C：创建

Create

```
create database 数据库名称;  -- 创建数据库
create database if not exists 数据库名称;  -- 判断不存在再创建：
create database 数据库名称 character set 字符集名;  -- 指定字符集：
```

##### 3.3.1.2 R：查询

Retrieve

```
show databases;  -- 查询所有数据库的名称
show create database 数据库名;  -- 查看某个数据库的字符集（编码），本意是查询某个数据库的创建语句
```

##### 3.3.1.4 D：删除

Delete

```
drop database 数据库名称;  -- 删除数据库
drop databse if exists 数据库名称;  -- 判断存在再删除
```

##### 3.3.1.5 使用数据库

```
select database();  -- 查询当前正在使用的数据库名称

use 数据库名称;  -- 使用数据库
```

#### 3.3.2 操作表

数据库数据类型有：
5. timestamp：时间戳类型，包含年月日时分秒，```yyyy-MM-dd HH:mm:ss```。如果不给这个字段赋值，或赋值为null，则默认使用当前的系统时间来自动赋值

##### 3.3.2.2 查询

```
desc 表名;  -- 查询表结构
```

##### 3.3.2.3 修改

```sql
alter table 表名 rename to 新的表名;  -- 修改表名

alter table 表名 character set utf8;  -- 修改表的字符集

alter table 表名 add 列名 数据类型;  -- 添加一列

alter table 表名 change 原列名 新列名 新类型;  -- 修改列名和类型
alter table 表名 modify 列名 新类型;  -- 只修改类型

alter table 表名 drop 列名;  -- 删除列
```

##### 3.3.2.4 删除

```
drop table 表名;
drop table if exists 表名;
```

### 3.4 DML：增删改表中数据

#### 3.4.1 添加数据

3. 除了数字类型和NULL，其他类型需要使用引号（单双均可）引起来
4. 在值前面加上N表示用Unicode编码，所有字符占2个字节



```
truncate table 表名;
```

#### 3.4.3 修改数据

```
update 表名 set 列名1 = 值1, 列名2 = 值2, ... [where 条件];
```

注意：如果不加条件，会修改所有值。



#### 3.5.1 语法

3. 计算列
一般可以使用四则运算计算一些列的值，如果有null参与，结果都为null。

```
ifnull(表达式1,表达式2);
```
表达式1为可能会出现null的字段，判断是否有null的字段名。如果字段为null，会替换为表达式2的值

#### 3.5.3 条件查询

+ 运算符
```
> < <= >= = <>  -- 【不等于有2种<>或<!=>，等于只有一个等号】

IS NULL  -- NULL不能用等于和不等于判断
IS NOT NULL

and或&&，推荐and，下同
or或||
not或！
```

#### 3.5.4 排序查询

```
order by 子句

即：
order by 排序字段1 排序方式1， 排序字段2 排序方式2...
```
排序方式：
  ASC：升序，默认
  DESC：降序

注意：
如果有多个排序条件，则当前面的条件值一样时，才会判断第二个条件。

#### 3.5.6 分组查询

```
group by 分组字段;  -- 用于需要分组的字段有重复，最后显示的结果中相同的进行合并
```

+ 分组之后查询的字段：分组字段、聚合函数

+ where和having的区别：
  1. where在分组之前进行限定，如果不满足条件，则不参与分组
  2. having在分组之后进行限定，如果不满足条件，则不会被查询出来
  3. where后不能跟聚合函数，having后可以进行聚合函数的判断

#### 3.5.7 分页查询

```
limit 开始的索引，每页查询的条数;  -- 从开始的索引开始，显示n条，索引从0开始
```

+ limit是一个MySQL的“方言”

## 4 约束

概念：对表中的数据进行限定，保证数据的正确性、有效性和完整性。

分类：

  1. 主键约束：primary key

  2. 非空约束：not null

  3. 唯一约束：unique

  4. 外键约束：foreign key

### 4.1 主键约束：primary key

含义：非空且唯一
+ 一张表只能有一个字段为主键

1. 创建表的时候添加：字段后面跟```primary key```
2. 删除主键：
```
alter table stu drop primary key;
```
3. 创建好的表添加主键：用修改命令，字段后面加```primary key```

+ 自动增长：如果某一列是数值类型的，使用```auto_increment```。如果填NULL，就会自动获得一个+1的数。关键字跟在字段后面就行

+ 删除：直接用修改命令

### 4.2 非空约束：值不能为null

```NOT NULL```

1. 创建表添加非空约束
创建表的时候，在字段后面加上```NOT NULL```

2. 创建表完后添加非空约束
修改命令

3. 删除非空约束
    用修改命令，不写NOT NULL
```
alter table stu modify name varchar(20)
```

### 4.3 唯一约束：值不能重复

```unique```

注意：唯一约束限定的列的值可以有多个null

1. 创建表的时候跟在字段后面
2. 创建表后添加唯一约束：修改的时候加载字段后面
3. 删除唯一约束：删除唯一索引
```
alter table stu drop index phone_number;
```

### 4.4 外键约束：foreign key

让表和表产生关系，从而保证数据的正确性

创建表时，可以添加外键：
```
create table 表名(
    ...
    外键列，
    constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称)
);
```


```
alter table stu drop foreign key 外键名称;  -- 删除外键

alter table stu add constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称);  -- 添加外键
```

## 7 事务


### 7.2. 事务的四大特征ACID

atomic consistency isolation durability

1. 原子性：不可分割的最小操作单位，要么同时成功，要么同时失败
2. 持久性：事务提交或回滚后，数据库会持久化的保存数据
3. 隔离性：多个事务之间相互独立
4. 一致性：事务操作前后，数据总量不变

### 7.3. 事务的隔离级别

多个事务操作同一批数据，会出问题：

   1. 脏读：一个事务，读取到另一个事务中没有提交的数据
   2. 不可重复读（虚读）：同一个事务中，两次读取到的数据不一样
   3. 幻读：一个事务操作数据表中所有记录，另一个事务添加了一条数据，则第一个事务查询不到自己的修改

隔离级别：
1. read uncommitted：会脏读、虚读、幻读
2. read committed（Oracle默认）：会虚读、幻读
3. repeatable read（MySQL默认）：幻读
4. serializable：没问题

隔离级别越高，效率越低

## 8 JDBC

### 8.1 JDBC使用流程

步骤：
1. 下载jar包，导包：mysql-connector
2. 注册驱动
3. 获取数据库连接对象 **Connection**
4. 定义**sql**
5. 获取执行sql语句的对象 **Statement**
6. 执行sql，接受返回结果
7. 处理结果
8. 释放资源

```
//1. 导包：建了libs文件夹，右键，add as library

//2. 注册驱动，mysql5后可以省略
Class.forName("com.mysql.jdbc.Driver");

//3. 获取数据库连接对象
Connection conn = DiverManager.getConnection("jdbc:mysql://localhost:3306/db3","root","password");

//4. 定义sql语句
String sql = "update account set balance = 500 where id = 1";

//5. 获取执行sql的对象
Statement stmt = conn.createStatement();

//6. 执行sql
int count = stmt.executeUpdate(sql);

//7. 处理结果

//8. 释放资源
stmt.close();conn.close();
```

#### 8.2.2 sql语句执行对象：Statement/PreparedStatement

Statement：执行sql的对象

##### 8.2.2.1 执行sql的方法

```
boolean execute(String sql)
	可以执行任意的sql【了解】

int executeUpdate
	执行DML语句（insert、update、delete）、DDL语句（create、alter、drop）
	返回值：影响的行数，>0说明执行成功，否则失败

ResultSet executeQuery(String sql)
	执行DQL语句（select）
```

##### 8.2.2.1 结果集对象：ResultSet

ResultSet：结果集对象，封装查询结果

```
游标向下移动一行：
boolean next();

初始游标位于第一行之前，第一次调用后移动到第一行。当当前行已经在最后一行以下，返回false，否则为true。


获取数据：
getXxx(参数);

Xxx代表数据类型，如getInt、getString。参数包括2种：
    int：列的编号，从1开始。
    String：列的名称


遍历：
while(rs.next()){
int id = rs.getInt(1);
...
}
```

##### 8.2.2.2 PreparedStatement：执行sql的对象

SQL注入问题：在拼接sql语句的时候，有一些sql的特殊关键字参与字符串的拼接，会造成安全问题

+ 解决：使用PreparedStatement

+ 预编译的SQL：参数使用```?```作为占位符

步骤：

1. 导包，注册驱动，获取数据库连接对象
2. 定义sql，注意这时用```?```作为占位符
3. 获取执行sql语句的对象，注意需要传入参数```Connection.prepareStatement(String sql)```
4. 给```?```赋值：
    方法：```setXXX(参数1,参数2)```
        参数1：```?```的位置编号，从1开始
        参数2：```?```的值
5. 执行sql，接受返回结果，不需要传递sql语句
6. 处理结果，释放资源

### 8.4 JDBC控制事务

使用Connection对象管理事务

### 8.5 数据库连接池DataSource

方法：
    获取连接：```getConnection()```
    归还连接：调用```Connection.close()```表示归还连接

#### 8.5.2 Druid

步骤：
1. 导入jar包（1个+数据库驱动）
2. 定义配置文件：可以用.properties，可以叫任意名称，可以放在任意目录下

```
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/learn
username=root
password=root
initialSize=5
maxActive=10
maxWait=3000
```



1. 获取数据库连接池对象：通过工厂类```DruidDataSourceFactory```来获取
2. 获取连接：getConnection

```
//加载配置文件
Properties pro = new Properties();
InputStream is = DruidDemp.class.getClassLoader().getResourceAsStream("wenjianming.properties");
pro.load(is);

//获取连接池，获取连接
DataSource sc = DruidDataSourceFactory.createDataSource(pro);
Connection conn = ds.getConnection();
```

### 8.6 Spring JDBC

Spring框架对JDBC的简单封装，提供了一个JDBCTemplate对象简化JDBC的开发。

步骤：
1. 导包
2. 创建JDBCTemplate对象，依赖于数据源DataSource

```
JdbcTemplate template = new JdbcTemplate(传入一个连接池);
```
3. 调用方法进行CRUD：

```
update()执行DML语句，增删改，sql语句里可以用？占位

queryForMap()查询结果，结果封装为map集合。只能查询1条记录
queryForList()查询结果，结果封装为list集合，list集合里的元素是Map，对应一条记录

query()查询结果，结果封装为JavaBean对象
queryForObject(sql,A.class)查询结果，结果封装为A的对象//这句在实际时候的时候有问题，别传A.class，传new BeanPropertyRowMapper<T>(T.class)

注意：
query()方法传入的第二个参数：
是一个接口：RowMapper，可以自己实现，返回一个需要的JavaBean对象，也可以用现成的
new BeanPropertyRowMapper<T>(T.class)
注意这里的JavaBean的变量都用包装类定义，不然null传入的时候会报错
```

## 9 Web概念概述

## 10 HTML

注释的写法：
```
<!-- 注释的内容 -->
```

### 11.2 CSS基本语法

```
选择器{
    属性名1：属性值1；
    属性名1：属性值1；
    ...
}
```

+ 注释：```/* */```

### 11.3 选择器

筛选具有相似特征的元素

#### 11.3.1 基础选择器

```
#id属性值{}
	id选择器：选择具体的id属性值的元素.多个属性用逗号隔开

标签名称{}
	元素选择器：选择具有相同标签名称的元素

.class属性值{}
	类选择器：选择具有相同的class属性值的元素
```

+ 一般设置id唯一，class可以多个共用
+ 优先级：id>类>元素

#### 11.3.2. 扩展选择器

```
*{}
	选择所有元素：

选择器1，选择器2{}
	并集选择器。【逗号】

选择器1 选择器2{}
	子选择器：筛选选择器1元素下的选择器2元素。【空格】

选择器1>选择器2{}
	父选择器：筛选选择器2的父元素选择器1。有属性first-child

元素名称[属性名=“属性值”]{}
	属性选择器：选择元素名称，属性名=属性值的元素

元素：状态{}
	伪类选择器：选择一些元素具有的状态。如超链接标签<a>上就常见。
    link：初始化的状态
    visited：被访问过的状态
    active：正在访问的状态
    hover：鼠标悬浮状态
```

## 12 JavaScript

**JavaScript = ECMAScript + JavaScript自己特有的东西（BOM + DOM）**

### 12.1 ECMAScript

客户端脚本语言的标准

##### 12.1.1.2. 注释

和java一样

##### 12.1.1.3. 数据类型：

+ 原始数据类型

  1. number：数字。整数/小数/NaN(not a number)
  2. string：字符串。没有字符。
  3. boolean：true/false
  4. null：对象为空
  5. undefined：未定义。如果一个变量没有给初始化的值，那么默认赋值为undefined。

+ 引用数据类型：对象

##### 12.1.1.5. 运算符

1. 一元运算符
在JS中，如果运算数不是运算符所要求的类型，那么JS引擎会自动的将运算数进行类型转换。
   + string转number：按字面值转换。如果不是数字，转换为NaN，NaN与任何数运算还是NaN。
   + boolean转number：true转为1，false转为0
4. 比较运算符
```===```：全等于
   + 类型相同，直接比较。字符串会按字典顺序，逐位比较。
   + 类型不同，先进行类型转换，再比较。

   + 全等于会先判断类型，类型不一样则直接返回false。
5. 逻辑运算符
    其他类型转boolean：
   + number：0或NaN为假，其他为真。
   + string：除了空字符串```""```，其他都是true。
   + null&undefined：都是false。
   + 对象：所有对象都是true。

#### 12.1.2. 基本对象

##### 12.1.2.1 Function：函数对象

3. 属性
```length：形参的个数```

4. 特点
   + 方法定义的时候，形参的类型不用写，返回值类型也不写
   + 方法是一个对象，如果定义名称相同的方法，会覆盖
   + 在JS中，方法的调用只与方法的名称有关，和参数列表无关
   + 在方法声明中有一个隐藏的内置对象：数组arguments，封装了所有的实际参数
##### 12.1.2.2 Array：数组对象

1. 创建
```
var arr = new Array(元素列表);

var arr = new Array(默认长度);

var arr = [元素列表];
```
2. 方法
```
join(参数)
	将数组中的元素按照指定的分隔符拼接成字符串（默认为逗号）

push()
	向数组的末尾添加一个或更多元素，并返回新的长度。
```
3. 属性
```length：数组的长度```
4. 特点
   + 在JS中，数组的元素的类型可变
   + 在JS中，数组的长度可变

##### 12.1.2.3 Boolean

##### 12.1.2.4 Date

1. 创建
```
var data = new Date();
```
2. 方法
```
toLocaleString()
	返回当前Date对象对应的时间本地字符串格式
getTime()
	获取毫秒值。
```

##### 12.1.2.5 Math

1. 创建
不用创建，直接使用。Math.方法名()

2. 方法
```
random():返回0~1之间的随机数。含0不含1
ceil(X)：向上取整
floor(X)：向下取整
round(x)：四舍五入
```
3. 属性
```PI```

##### 12.1.2.6 Number

##### 12.1.2.7 String

##### 12.1.2.8 RegExp：正则表达式对象

正则表达式：

+ 单个字符：[ ]
如```[a] [ab] [a-zA-Z0-9_]=\w \d```
+ 量词符号：
```
? 
	0/1 
*
	任意
+
	1+
{m,n}
	m到n位，包含两边
```
+ 开始结束符号：```^ $```

RegExp：

1. 创建
```
var reg = new RegExp("正则表达式");//这里要注意，\表示转义字符，\w要写成\\w

var reg = /正则表达式/;常用这个
```
2. 方法
```
test(参数)
	验证指定的字符串是否符合正则表达式
```

##### 12.1.2.9 Global：全局对象

其中封装的方法不需要对象，直接调用。```方法名();```
```
encodeURI():URI编码
decodeURI():URI解码

encodeURIComponent():URI编码，冒号等也编码
decodeURIComponent():URI解码，冒号等也编码

parseInt():字符串转为数字。会逐一判断每个字符是否是数字，直到不是数字为止，将前边数字部分转为number

isNaN():判断一个值是否是NaN。NaN六亲不认，参与的比较全是false

eval：将字符串转换为JS脚本代码来执行
```

URL对中文进行编码，一个百分号是一个字节

### 12.2 BOM

+ 概念：Browser Object Model 浏览器对象模型
+ 将浏览器的各个组成部分封装成对象。

Window：窗口对象
Navigator：浏览器对象
Screen：显示器屏幕对象
History：历史记录对象
Location：地址栏对象

#### 12.2.1 Window

窗口对象

##### 12.2.1.1 创建

不需要创建

##### 12.2.1.2 方法

1. 与弹出框有关的方法
```
alert()
	显示带有一段消息和一个确认按钮的警告框

confirm()
	显示带有一段消息以及确认按钮和取消按钮的对话框
	如果用户点确定，方法返回true，用户点取消，方法返回false

prompy()
	显示可提示用户输入的对话框
	返回值：用户的输入
```
2. 与打开关闭有关的方法
```
close()
	关闭浏览器窗口
    谁调用，关闭谁
open()
    打开一个新的浏览器窗口
    返回新的window对象
```
3. 与定时器有关的方法
```
setTimeout()
    在指定的毫秒数后调用函数或计算表达式
    参数
        1. js代码或方法对象
        2. 毫秒值
    返回值：唯一标识，用于取消定时器

clearTimeout()
    取消setTimeoutsetTimeout()方法设置的timeout

setInterval()
	按指定的周期（毫秒计）来调用函数或计算表达式

clearInterval()
	取消setInterval()方法设置的timeout
```

##### 12.2.1.3 属性

1. 获取其他BOM对象
```
history
location
Navigator
Screen
```
2. 获取DOM对象
```
document
```
##### 12.2.1.4 特点

+ window对象不需要创建，可以直接使用。
```
window.方法名()
```
+ window引用也可以省略，直接
```
方法名()
```

#### 12.2.4. History：历史记录对象

##### 12.2.4.1 创建（获取）

```
window.history
或
history
```

##### 12.2.4.2. 方法

```
back()		
	加载history列表中的前一个URL

forward()	
	加载history列表中的后一个URL

go(参数)	   
	加载history列表中的某个具体页面
    参数：
	    正数：前进几个历史记录，go(1)=forward()
    	负数：后退几个历史记录
```

##### 12.2.4.3. 属性

```
length
	返回当前窗口历史列表中的URL数量
```

#### 12.2.5. Location：地址栏对象
##### 12.2.5.1. 创建（获取）

```
window.location
或
location
```

##### 12.2.5.2. 方法

```
reload
	重新加载当前文档。刷新
```

##### 12.2.5.3. 属性

```
href
	设置或返回完整的URL
```

### 12.3 DOM

+ 概念：Document Object Model 文档对象模型
+ 功能：控制html文档的内容

W3C DOM 标准被分为3个不同的部分：

+ 核心 DOM：针对任何结构化文档的标准模型
+ XML DOM：针对XML文档的标准模型
+ HTML DOM：针对HTML文档的标准模型

#### 12.3.2 核心DOM模型

##### 12.3.2.1 Document：文档对象

1. 创建（获取）
在html dom模型中，可以使用window对象来获取

2. 方法

+ 获取Element对象
```
getElementById()
	根据id属性值获取元素对象，id属性值一般唯一

getElementByTagName()
	根据元素名称获取元素对象们，返回值是一个数组

getElementByClassName()
	根据Class属性获取元素对象们，返回值是一个数组

getElementByName()
	根据name属性获取元素对象们，返回值是一个数组
```

##### 12.3.2.2 Element：元素对象

1. 创建（获取）：通过document来获取和创建
2. 方法
```
removeAttribute()：删除属性

setAttribute()：设置属性
```

##### 12.3.2.4 其他

超链接
```
href = "javascript:void(0)"; //可以被点击的样式，但是不跳转
```
+ value属性获取内容
+ this获取当前对象

#### 12.3.3 HTML DOM

1. 标签体的设置和获取：innerHTML
```
var div = document.getElementById("div1");
var innerHTML = div.innerHTML;
```
2. 使用html元素对象的属性
```
div.innerHTML = "<input type='text'>";
```
3. 控制元素样式
   + 使用元素的style属性来设置（每个元素都有这个属性，后面直接点CSS的属性） 
   + 提前定义好类选择器的样式，通过元素的className属性来设置其class属性值
```
div.style.border="1px solid red";

div.className = "cls";
```

## 13 事件

功能：某些组件被执行了某些操作后，触发某些代码的执行。

### 13.1 简单流程

如何绑定事件：
1. 直接在html标签上，指定事件的属性（操作），属性值就是js代码
```
<a href="..." onclick="js代码">
```

2. 通过js获取元素对象，指定事件属性，设置一个函数
```
document.getElementById("01").onclick=function(){
    ...
}
```

debug：正常打断点，然后在浏览器按下F12，在Console里看

### 13.3 常见的事件

#### 13.3.1 点击事件

```
onclick：单击事件

ondbclick：双击事件
```

#### 13.3.2. 焦点事件

```
onblur:失去焦点：一般用于表单校验

onfocus:元素获得焦点
```

#### 13.3.3. 加载事件

```
onload
	一张页面或一幅图像完成加载
	window.onload = ..
```

#### 13.3.7. 表单事件

```
onsubmit
	确认按钮被点击，可以阻止表单的提交，return false就会阻止提交。
	如果写在onclick属性里，要写return checkForm()
```

## 14 Bootstrap

+ 概念：一个前端开发的框架。
+ 好处：
1. 定义了很多CSS样式和JS插件。开发人员可以直接使用这些样式和插件得到丰富的页面效果。
2. 响应式布局：同一套页面可以兼容不同分辨率的设备。

### 14.2 响应式布局

+ 同一套页面可以兼容不同分辨率的设备
+ 实现：依赖于栅格系统，将一行平均分成12个格子，可以指定元素占几个格子。

## 15 XML

### 15.1 概念

+ Extensible Markup Language 可扩展标记语言
+ 可扩展：标签都是自定义的。

+ 功能：存储数据
  1. 配置文件
  2. 在网络中传输
  
+ 与html的区别
  1. xml的标签是自定义的，html是预定义
  2. xml语法严格，html语法松散
  3. xml存储数据，html展示数据

### 15.2 语法

#### 15.2.1 基本语法

1. xml文档的后缀名：.xml
2. xml第一行必须定义为文档声明【空行都不行】
3. xml文档中有且仅有一个根标签
4. 属性值必须用引号（单双均可）引起来
5. 标签必须正确关闭
6. xml标签名称区分大小写

#### 15.2.2 组成部分

1. 文档声明
```
<?xml 属性列表 ?>
```
属性列表
```
version
	版本号，写1.0。必须写的

encoding
	编码方式。告诉解析引擎当前文档使用的字符集，默认值ISO-8859-1【IDE会自己识别，写上就行】

standalone
	是否独立。可以不设置，现在很多yes也可以依赖
    yes
    	不依赖其他文件
    no
    	以来其他文件
```

2. 指令（了解）：结合CSS的

3. 标签：名称自定义
   规则：名称可以包含字母、数字、其他字符。不能以数字或标点开始，不能以xml开始，不能包含空格

4. 属性：
   id属性值唯一

5. 文本
   CDATA区：该区域的字符会原样展示。
```
<![CDATA[展示的数据]]>
```

#### 15.2.3 约束：规定xml文档的书写规则

作为框架的使用者：
1. 能够在xml中引入约束文档
2. 能够简单的读懂约束文档

分类：
1. DTD：一种简单的约束技术
2. Schema：一种复杂的约束技术

##### 15.2.3.1 DTD

引入DTD文档到xml文档中

内部dtd：将约束规则定义在xml文档中
外部dtd：将约束的规则定义在外部的dtd文件中

本地：
```
<!DOCTYPE 根标签名 SYSTEM “dtd文件的位置”>
```
网络：
```
<!DOCTYPE 根标签名 SYSTEM “dtd文件名字” “dtd文件的位置URL”>
```

##### 15.2.3.2 Schema


```
<taglib xmlns="http://java.sun.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-jsptaglibrary_2_1.xsd"
        version="2.1">
```

location行是资源的位置

然后xmlns：xxx，是起前缀

### 15.3 解析

+ xml常见的解析器：
  3. Jsoup：本身是解析HTML的。

#### 16.3.1 目录结构

##### 16.3.1.1 java动态项目的目录结构
```
--项目的根目录
--WEB-INF目录：
    --web.xml：web项目的核心配置文件
    --classes目录：放置字节码文件的目录
    --lib目录：放置依赖的jar包
```

+ 端口号
+ https是443



4. 配置servlet：WEB-INF里的web.xml里，写：
```
<servlet>
    <servlet-name>demo1名字</servlet-name>
    <servlet-class>全类名</servlet-class> 
</servlet>

<servlet-mapping>
    <servlet-name>demo1</servlet-name>
    <url-pattern>/资源路径<url-pattern>
</servlet-mapping>
```

### 17.3 Servlet3.0

好处：

1. 支持注解配置，可以不需要web.xml

1. 在类上使用@WebServlet注解，进行配置

```
@WebServlet(urlPattern="/demo")

也可以直接写
@WebServlet("/demo")
```

### 

+ servlet包一般起名是：com.xxx.web.servlet
+ 每个项目都可以起一个虚拟目录



可以配置执行Servlet的创建时机。
```
<servlet>
    ...
    <load-on-startup>  </load-on-startup>
</servlet>
```

+ 上面这个标签的值是负数：第一次访问时被创建。默认值是-1
  0或正数：服务器启动时，创建

Servlet的init方法只执行一次，说明在内存中只存在一个Servlet对象

+ 多个用户同时访问时，可能存在线程安全问题
  解决：尽量不要在Servlet中定义成员变量。即使定义了成员变量，也不要修改。

### 17.4 体系结构

+ Servlet：接口

+ GenericServlet：抽象类，实现了Servlet接口

+ HTTPServlet：抽象类，继承了GenericServlet

说明：

+ GenericServlet：将Servlet接口中的其他方法做了默认空实现，只将service方法作为抽象方法
  将来定义Servlet类时，可以继承GenericServlet，实现service方法即可。如果需要写别的方法，覆写就好。

+ HTTPServlet：对http协议的一种封装，简化操作【比如判断传输的方式是get还是post】
   1. 定义类继承HTTPServlet
   2. 覆写doGet/doPost方法


### 17.5 Servlet相关配置

1. urlpattern：Servlet访问路径。一个Servlet可以定义多个访问路径。
```
@WebServlet({"/1","/2","/3"})
```
2. 路径定义规则：
```
1. /xxx
2. /xxx/xxx			//如果用*通配符，优先级是最低的
3. *.do				//千万注意,前面没有/
```

## 18 HTTP
+ Hyper Text Transfer Protocol：超文本传输协议

+ 传输协议：定义了，客户端和服务器通信时，发送数据的格式

特点：

 1. 基于TCP/IP的高级协议
 2. 默认端口：80
 3. 基于请求/响应模型的：一次请求对应一次响应
 4. 无状态的：每次请求之间互相独立，不能交互数据

历史版本：
1.0：每一次请求响应都会建立新的连接
1.1：复用连接【还有很多别的区别】

### 18.1 请求消息

+ 请求消息数据格式
    请求行
    请求头
    请求空行
    请求体

#### 18.1.1 请求行

```
请求方式 请求url 请求协议/版本
GET /login.html HTTP/1.1
```

#### 18.1.2. 请求头

```
请求头名称：请求头值1，请求头值2
```

#### 18.1.3. 请求空行

空行，分割POST请求的请求头和请求体

#### 18.1.4. 请求体（正文）

封装POST请求消息的请求参数

### 18.2 Request对象

#### 18.2.1 request对象和response对象的原理

两个对象都是由服务器tomcat创建的，我们来使用它们

#### 18.2.3 request功能

**1. 获取请求参数通用方式**

```
String getParameter(String name);
	根据参数名称获取参数值【常用】

String[] getParameterValues(String name);
	获取参数值的数组，多用于复选框，参数名称相同的

Enumeration<String> getParameterNames();
	获取所有请求的参数名称

Map<String,String[]> getParameterMap();
	获取所有参数的map集合，键值对【常用】
```
中文乱码问题：
+ get方式：tomcat 8 已经解决了
+ post方式：会乱码
解决：在获取参数前，设置request的编码
```
request.setCharacterEncoding("utf-8");【干脆每次都写，以防万一】
```

**2. 请求转发：一种在服务器内部的资源跳转方式**

步骤：
1. 通过request对象获取请求转发器对象
```
RequestDispatcher getRequestDispatcher(String path);
```
2. 使用RequestDispatcher对象来进行转发
```
forward(ServletRequest request, ServletResponse response);
```

+ 特点
  1. 浏览器地址栏路径不发生变化
  2. 只能转发到当前服务器内部资源中
  3. 转发是一次请求
  

**3. 共享数据**
+ 域对象：一个有作用范围的对象，可以在范围内共享数据
+ request域：代表一次请求的范围，一般用于请求转发的多个资源中共享数据

方法：
```
void setAttribute(String name, Object obj);存储资源

Object getAttribute(String name);通过键获取值

void removeAttribute(String name);通过键移除键值对
```

**4. 获取ServletContext**

```
ServletContext getServletContext();
```

##### 18.2.3.3 案例

login.html中form表单的action路径的写法：
虚拟目录+Servlet的资源路径

#### 18.3.1 响应行
```
协议/版本 响应状态码 状态码描述
```
+ 响应状态码：服务器告诉客户端浏览器本次请求和响应的一个状态。
  状态码都是3位数字
```
1xx：服务器接收客户端消息，但是没有接收完成，等待一段时间后，发送1xx状态码
2xx：成功。如，200
3xx：重定向。如：302重定向，304访问缓存
4xx：客户端错误。如：404请求路径没有对应的资源，405请求方式没有对应的doXxx方法
5xx：服务器端错误。如：500服务器内部出现异常
```
## 18.4 Response对象

### 18.4.4 重定向

重定向：资源跳转的方式

```
等价于：
response.sendRedirect("/day15/demo2");
```

+ 重定向的特点：redirect
  1. 地址栏发生变化
  2. 重定向可以访问其他站点（服务器）的资源
  3. 重定向是两次请求。不能使用request对象来共享数据

+ 转发的特点：forward
  1. 转发地址栏路径不变
  2. 转发只能访问当前服务器下的资源
  3. 转发是一次请求，可以使用request对象来共享数据

### 18.4.5 路径的写法

+ 相对路径：
+ 绝对路径：
```
本地可以省略ip和端口，/day15/demo2也是绝对路径
```

+ 规则：判断定义的路径给谁用？判断请求从哪里发出
   + 给客户端使用：需要加虚拟目录（项目的访问路径）
     建议虚拟目录动态获取：request.getContextPath()
     重定向
   + 给服务器使用：不需要加虚拟目录
     转发

### 18.4.6 其他

+ 乱码问题：
  设置响应头里的content-type。
  获取流之前设置
```
response.setContentType("text/html;charset=utf-8");
```

+ 验证码问题：
  切换验证码：onclick事件里，改变img的src，相当于重新随机一张验证码。但是有缓存问题，为了避免：
```
src = "/.../...?"+data;
```
data是时间戳，?表示传了个参数。data = new Data().getTime()

## 19 ServletContext对象

+ 概念：代表整个web应用，可以和程序（Servlet）的容器（服务器Tomcat）来通信

+ 获取：```request.getServletContext()```

+ 功能：
1. 获取MIME类型
    MIME类型：在互联网通信过程中定义的一种文件数据类型
    格式：```大类型/小类型```  如：```text/html``` ```image/jpeg```
```
String getMimeType(String file)
```
2. 域对象：共享数据
```
void setAttribute(String name, Object obj);存储资源
Object getAttribute(String name);通过键获取值
void removeAttribute(String name);通过键移除键值对
```

+ ServletContext对象范围：所有用户所有请求的数据
3. 获取文件的真实（服务器）路径
```
String getRealPath(String path)


web目录下的资源访问:
String b = context.getRealPath("/b.txt");

WEB-INF目录下的资源访问:
String c = context.getRealPath("/WEB-INF/c.txt");

src目录下的资源访问，或通过classloader:
String a = context.getRealPath("/WEB-INF/classes/a.txt");
```

### 19.1 案例

+ 弹窗下载图片
  设置响应头content-disposition【这里还设置了content-type】

+ 问题：中文文件名。
  解决：根据客户端的浏览器不同，用不同的方式编码filename【IE：URL，火狐：BASE64，这种工具类有很多，不用自己写】

## 20 会话技术

1. 会话：一次会话中包含多次请求和响应
    一次会话：浏览器第一次给服务器资源发送请求，会话建立，直到有一方断开为止。

2. 功能：在一次会话的范围内，多次请求间共享数据
3. 方式
   + 客户端会话技术：**Cookie**
   + 服务器端会话技术：**Session**

### 20.1 Cookie

概念：客户端会话技术，将数据保存在客户端

#### 20.1.1 快速入门

使用步骤：
```
new Cookie(String name, String value);	创建Cookie对象，绑定数据

response.addCookie(Cookie cookie);	发送Cookie对象

Cookie[] request.getCookies();	获取Cookie，拿到数据
```
```
cookie.getName()
cookie.getValue()
cookie.setValue()
```

#### 20.1.4. cookie的细节

1. 一次可不可以发送多个cookie？

   可以
   可以创建多个Cookie对象，然后调用多次addCookie方法

2. cookie在浏览器中保存多长时间？

   默认情况下，当浏览器关闭后，Cookie数据被销毁

   持久化存储
```
setMaxAge(int seconds)
	正数：将Cookie数据写到硬盘文件中，持久化存储。并制定cookie存活时间，时间到后，cookie文件自动失效
	负数：默认值
	零：删除cookie信息
```

3. cookie能不能存中文？

   在tomcat 8 之前，cookie中不能直接存储中文，需要编码
   在tomcat 8 之后，cookie支持中文数据，但是特殊字符还是需要编码

4. cookie共享问题
   1. 一个tomcat服务器中，部署了多个web项目
      默认情况下不能。
```
setPath(String path)；
设置cookie的获取范围。默认情况下，是当前的虚拟目录，如果要共享，设置成"/"
```

   2. 不同的tomcat服务器间cookie共享问题。默认不能
```
setDomain(String path);
如果一级域名相同，那么多个服务器间cookie可以共享。如
setDomain(".baidu.com");
```

#### 20.1.5. Cookie的特点和作用

1. cookie存储数据在客户端浏览器
2. 浏览器对于单个cookie的大小有限制（4kb）以及对同一个域名下的总cookie数量也有限制（20个）

**作用：**

1. cookie一般用于存储少量的不太敏感的数据
2. 在不登录的情况下，完成服务器对客户端的身份识别

### 20.2 Session

服务器端会话技术，在一次会话的多次请求间共享数据，将数据保存在服务器端的对象中。HttpSession

#### 20.2.1 快速入门

```
HttpSession session = request.getSession()	获取HTTPSession对象

使用HTTPSession对象
getAttribute、set、remove	
```

#### 20.2.3. 原理

session的实现是依赖于Cookie的

#### 20.2.4. 细节

1. 当客户端关闭后，服务器不关闭，两次获取的session默认不是同一个
   如果需要相同，可以创建Cookie，设置键为JSESSIONID，设置值为session.getId()，设置存活时间，让cookie持久化保存

2. 客户端不关闭，服务器关闭后，两次获取的session不是同一个
   但是要确保数据不丢失，tomcat会自动完成以下工作【IDEA内不行，启动前会删掉work目录，活化不了】
   + session的钝化：
    在服务器正常关闭之前，将session对象序列化到硬盘上
   + session的活化：
    在服务器启动后，将session文件转化为内存中的session对象

3. session什么时候被销毁？
   1. 服务器关闭
   2. session对象调用方法```invalidate()```
   3. session默认失效时间：30分钟，可以在web.xml里修改

#### 20.2.5. session的特点

1. session用于存储一次会话的多次请求的数据，存在服务器端
2. session可以存储任意类型，任意大小的数据

**session和cookie的区别：**【主菜，小甜点】

1. session存储数据在服务器端，cookie在客户端
2. session没有数据大小限制，cookie有
3. session数据安全，cookie相对不安全

## 21 JSP

+ Java Server Pages：java服务器端页面
可以理解为：一个特殊的页面，其中既可以定义html标签，又可以定义java代码。
可以用于简化书写

### 21.1 原理

JSP本质上就是一个Servlet

### 21.2 JSP脚本：JSP定义Java代码的方式

```
1. <%  代码  %>：定义的java代码，在service方法中。
2. <%!  代码  %>：定义的java代码，会在jsp转换后的java类的成员位置。
3. <%=  代码  %>：会直接输出到页面上，会转换为service方法内的print的内容。
```
### 21.4 注释

1. html注释```<!-- -->```只能注释html代码片段，被注释的内容依旧会被写到response里
2. jsp注释```<%-- --%>```可以注释所有。

在代码里面java的注释依旧可以使用

### 22 EL表达式

+ Expression Language 表达式语言

+ 替换和简化JSP页面中java代码的编写

```
${表达式}
```

在JavaScript里也可以用EL表达式

#### 22.1.2 获取值

el表达式只能从域对象中获取值

```
${域名称.键名}
```
## 23 JSTL

+ JavaServer Pages Tag Library JSP标准标签库
  是由Apache组织提供的开源的免费的jsp标签
+ 作用：用于简化和替换JSP页面上的java代码

## 27 Filter：过滤器

+ javaweb的三大组件：Servlet、Filter、Listener

+ web中的过滤器：当访问服务器的资源时，过滤器可以将请求拦截下来，完成一些特殊功能。

+ 过滤器的作用：
一般用于完成通用的操作。如：登录验证、统一编码处理、敏感字符过滤...

### 27.1 快速入门

1. 定义一个类，实现接口Filter【javax.servlet】
2. 复写方法
3. 配置拦截路径
+ web.xml
```
<filter>
    <filter-name>demo1</filter-name>
    <filter-class>全类名</filter-class>
</filter>
<filter-mapping>
    <filter-name>demo1</filter-name>
    <url-pattern>拦截路径</url-pattern>
</filter-mapping>
```
+ 注解
```
@WebFilter("/*")

在doFilter里
chain.doFilter(req,resp) //放行

可以像改Servlet模板一样更改模板
```

### 27.2 细节

#### 27.2.1 过滤器执行流程

1. 执行过滤器
2. 执行放行后的资源
3. 回来执行过滤器放行代码下边的代码

#### 27.2.2 过滤器生命周期方法

1. init：在服务器启动后，会创建Filter对象，然后调用init方法，只执行一次。用于加载资源
2. doFilter：每一次请求被拦截资源时，会执行。执行多次
3. destroy：在服务器关闭后，Filter对象被销毁。如果服务器是正常关闭，则会执行destroy方法。只执行一次。用于释放资源

#### 27.2.3 过滤器配置详解

#### 27.2.3.1 拦截路径配置：

1. 具体资源路径：```/index.jsp```	只有访问index.jsp资源时，过滤器才会被执行
2. 拦截目录：```/user/*```	访问/user下的所有资源时，过滤器都会被执行
3. 后缀名拦截：```*.jsp```	访问所有后缀名为jsp资源时，过滤器都会被执行
4. 拦截所有资源：```/*```	访问所有资源时，过滤器都会被执行

#### 27.2.3.2 拦截方式配置：

1. 注解配置
设置dispatchTypes属性【可以传入数组】
   + REQUEST：默认值。浏览器直接请求资源
   + FORWARD：转发访问资源
   + INCLUDE：包含访问资源【没讲】
   + ERROR：错误跳转资源【没讲】
   + ASYNC：异步访问资源【没讲】

2. web.xml配置
设置```<dispatcher></dispatcher>```标签即可【在```<filter-mapping>```里】

### 27.3 过滤器链（配置多个过滤器）

+ 执行顺序：如果有两个过滤器：过滤器1和过滤器2
   1. 过滤器1
   2. 过滤器2
   3. 资源执行
   4. 过滤器2
   5. 过滤器1

+ 过滤器先后顺序问题：
   1. 注解配置：按照类名的字符串比较规则比较，值小的先执行
        如：AFilter和BFilter，AFilter先执行
   2. web.xml配置：```<filter-mapping>```谁定义在上边，谁先执行

## 28 代理模式

设计模式：一些通用的解决固定问题的方式

解决敏感词过滤问题可以用到的两种设计模式：装饰模式和代理模式


### 28.1 概念

+ 真实对象：被代理的对象
+ 代理对象
+ 代理模式：代理对象代理真实对象，达到增强真实对象功能的目的

### 28.2 实现方式：

+ 静态代理：有一个类文件描述代理模式
+ 动态代理：在内存中形成代理类

+ 实现步骤：
   1. 代理对象和真实对象实现相同的接口
   2. 代理对象 = Proxy.newProxyInstance();
   3. 使用代理对象调用方法
   4. 增强方法

+ 增强方式：
   1. 增强参数列表
   2. 增强返回值类型
   3. 增强方法体执行逻辑


### 28.3 动态代理

1. 创建真实对象
2. 动态代理增强真实对象

#### 28.3.1 创建代理对象

```
Proxy.newProxyInstance()
```
传入三个参数：固定写法
1. 类加载器
2. 接口数组
3. 处理器

```
真实对象接口 代理对象 =(真实对象接口)Proxy.newProxyInstance(req.getClass().getClassLoader(), req.getClass().Interface， new InvocationHandler(){
	@Override
	public Object invoke(Object proxy, Method method, Object[] args) throws Trowable{
		Object obj = method.invoke(真实对象，args)
		return obj;		
	}
})
```
#### 28.3.2 invoke方法

```
@Override
	public Object invoke(Object proxy, Method method, Object[] args) throws Trowable{
		Object obj = method.invoke(真实对象，args)
		return obj;		
	}
```

+ 代理逻辑部分：代理对象调用的所有方法都会触发该方法执行
+ 参数：
   1. proxy：代理对象
   2. method：代理对象调用的方法，被封装为的对象
   3. args：代理对象调用的方法，传递的实际参数

#### 28.3.3 代理对象调用方法

在一个Filter里的doFilter写：

1. 建个代理，返回代理对象为proxy_req，然后放行的时候传proxy_req进去。
2. 代理内部：
   + 判断方法是否是xxx方法【getParameter/getParameterMap/getParameterValue】
   + 获取返回值
   + 替换返回值
```
ServletRequest proxy_req = (ServletRequest) Proxy.newProxyInstance(req.getClass().getClassLoader(), req.getClass().Interface， new InvocationHandler(){

	@Override
	public Object invoke(Object proxy, ...){
	
    	method.getName().equals(...);	//判断方法名
    	
        String value = (String) method.invoke(req,args);	//获取返回值

		//替换返回值
        if(value != null){
            for(String str :list){
                if(value.contains(str)){
                    value = value.replaceAll(str,"***");
                }
            }
        }
        
        return value;
	}
	
})
```

#### 28.3.4 在init里加载资源

```
ServletContext servletContext = config.getServletContext()

String realPath = servletContext.getRealPath("WEB-INF/classes/敏感词汇.txt")//txt是GBK的

BufferedReader br = new BufferedReader(new FileReader(realPath));//本地的流，默认GBK的流

String line = null;
while((line=br.readLine())!=null){
	list.add(line);//list定义在外面
}

br.close();
```

## 29 Listener：监听器

web的三大组件之一

### 29.1 事件监听机制

+ 事件：一件事情
+ 事件源：事件发生的地方
+ 监听器：一个对象
+ 注册监听：将事件、事件源、监听器绑定在一起。当事件源上发生某个事件后，执行监听器代码

### 29.2 ServletContextListener

+ ServletContextListener：监听ServletContext对象的创建和销毁

+ 主要用于加载资源文件

## 30 JQuery

+ 一个JavaScript框架。简化JS开发。
+ JavaScript框架：本质上就是一些JS文件，封装了JS的原生代码

### 30.1 快速入门

1. 下载JQuery
   + 带min和不带min：不带min的只有一行，缩小体积，加载更快
2. 导入JQuery的js文件
3. 使用：```$(选择器)```【EL表达式是大括号{}】

获得对象后，获取html内容：```$(选择器).html()```
```JS：innerHTML```

### 30.2 JQuery对象和JS对象区别与转换

1. JQuery对象在操作时，更加方便
2. JQuery对象和JS对象方法不通用
3. 两者相互转换
   js -->JQuery：```jq对象[索引]```或者```jq对象.get(索引)```
   JQuery -->js：```$(js对象)```

### 30.3 选择器：筛选具有相似特征的元素（标签）

#### 30.3.1 基本语法学习

1. 事件绑定
```
$("#button").click(function(){...})
```

2. 入口函数
```
$( funtion(){

} )
```
+ dom文档加载完成之后执行该函数中的代码
+ 相当于```window.onload = function(){...}```
+ 区别：```window.onload```只能写一个，多个会覆盖；``` $( funtion )```可以写多个

3. 样式控制
```
$("#id").css("background-color","red")
$("#id").css("backgroundColor","red")//这个按住ctrl，backgroundColor上会有小手，如果写错就没有
```

#### 30.3.2 基本选择器

1. 标签选择器
```
$("html标签名") 		获得所有匹配标签名称的元素
```
2. id选择器
```
$("#id的属性值")		获得与指定id属性值匹配的元素
```
3. 类选择器
```
$(".class的属性值")		获得与指定的class属性值匹配的元素
```
4. 并集选择器
```
$("选择器1,选择器2,...")
```

#### 30.3.3 层级选择器

1. 后代选择器
```
$("A B ")			选择A元素内部的所有B元素【包括孙子等等】
```
2. 子选择器
```
$("A > B")			选择A元素内部的所有B子元素【只有儿子】
```

#### 30.3.2.4 属性选择器

1. 属性名称选择器
```
$("A[属性名]")			包含指定属性的选择器
```
2. 属性选择器
```
$("A[属性名='值']")		包含指定属性等于指定值的选择器
    !=：属性不等于和不包含该属性的
    ^=：属性以某些值开始
    $=：属性以某些值结尾
    *=：属性包含某些值
```
3. 复合属性选择器
```
$("A[属性名='值'][]...")		包含多个属性条件的选择器
```

#### 30.3.2.5 过滤选择器

1. 首元素选择器
```
:first					获得选择的元素中的第一个元素 $("div:first")
```
2. 尾元素选择器
```
: last					获得选择的元素中的最后一个元素
```
3. 非元素选择器
```
:not(selector)			不包括指定内容的元素
```
4. 偶数选择器
```
:even					偶数，从0开始计数
```
5. 奇数选择器
```
:odd					奇数，从0开始计数
```
6. 等于索引选择器
```
:eq(index)				指定索引元素
```
7. 大于索引选择器
```
:gt(index)				大于指定索引元素
```
8. 小于索引选择器
```
:lt(index)				小于指定索引元素.
```
9. 标题选择器
```
:header					获得标题（h1~h6）元素，固定写法
```

#### 30.3.2.6 表单过滤选择器

1. 可用元素选择器
```
:enabled				获得可用元素
```
2. 不可用元素选择器
```
:disabled				获得不可用元素
```
3. 选中选择器
```
:checked				获得单选/复选框选中的元素
```
4. 选中选择器
```
:selected				获得下拉框选中的元素
```

+ val()方法，相当于JS的value属性，改变值

+ 下拉列表select选中个数的获取，注意要用option：
```$("#job > optiion:selected").length```

### 30.4 DOM操作

#### 30.4.1 内容操作

```
html()
	获取/设置元素的标签体内容
	<a><font>内容</font></a> --> <font>内容</font>

text()
	获取/设置元素的标签体纯文本内容
	<a><font>内容</font></a> --> 内容

val()
	获取/设置元素的value属性值
```

+ 设置时，往里传参。text设置的时候和html一样，都会把最外层标签里面的全替换掉

#### 30.4.2 属性操作

##### 3.4.2.1 通用属性操作
```
attr()
	获取/设置元素的属性

removeAttr()
	删除属性

prop()
	获取/设置元素的属性

removeProp()
	删除属性
```

+ 设置时传2个参数

+ 其中attr和prop的区别：
   1. 如果操作的是元素的固有属性，则建议使用prop【checkBox的checked和option的selected用attr获取不到】
   2. 如果操作的是元素的自定义的属性，则建议使用attr

##### 3.4.2.2 对class属性操作
```
addClass()
	添加class属性值

removeClass()
	删除class属性值

toggleClass()
	切换class属性值【存在则删除，不存在则添加】

css()
	设置css
```

#### 30.4.3 CRUD操作【移动】

```
append()
	父元素将子元素追加到末尾
    对象1.append(对象2)：将对象2添加到对象1元素内部，并且在末尾

prepend()
	父元素将子元素追加到开头
    对象1.prepend(对象2)：将对象2添加到对象1元素内部，并且在开头

appendTo()
    对象1.appendTo(对象2)：将对象1添加到对象2元素内部，并且在末尾

prependTo()
    对象1.prepenTo(对象2)：将对象1添加到对象2元素内部，并且在开头



after()
	添加元素到元素后边
    对象1.after(对象2)：将对象2添加到对象1后边。对象1和对象2是兄弟关系

before()
	添加元素到元素前边
    对象1.before(对象2)：将对象2添加到对象1前边。对象1和对象2是兄弟关系

insertAfter()
    对象1.insertAfter(对象2)：将对象1添加到对象2后边。对象1和对象2是兄弟关系

insertBefore()
    对象1.insertBefore(对象2)：将对象1添加到对象2前边。对象1和对象2是兄弟关系



remove()
	移除元素
    对象.remove()：将对象删除掉

empty()
	清空元素的所有后代元素
    对象.empty()：将对象的后代元素全部清空，但是保留当前对象以及其属性节点

clone()
	复制一个
```

### 30.6 遍历

#### 30.6.1 js的遍历方式

```
for(初始化值;循环结束条件;步长)
```

#### 30.6.2 jq的遍历方式

1. **```jq对象.each(callback)```**
```
jQuery对象.each(function(index,element){});
    index：元素在集合中的索引
    element：集合中的每一个元素对象

    this：集合中的每一个元素对象【JS对象】前两个可以一起不写

    回调函数返回值
        true：如果当前function返回false，则结束循环。break
        false：如果当前function返回true，continue
```
2. **```$.each(Object,[callback])```**
```
$.each(Object,[callback])
```
3. **```for...of```**

```
for(元素对象 of 容器对象)
	jquery3.0版本之后提供的方式
```

### 30.7 事件绑定

#### 30.7.1 jQuery标准的绑定方式

```
jq对象.事件方法(回调函数);
```
+ 注：如果调用事件方法，不传递回调函数，则会触发浏览器默认行为。
```
表单对象.submit();//让表单提交
```

#### 30.7.2. on绑定事件/off解除绑定

```
    jq对象.on("事件名称",回调函数)
    jq对象.off("事件名称")
        如果off方法不传递任何参数，则将组件上的所有事件全部解锁
```

#### 30.7.3. 事件切换：toggle

```
jq对象.toggle(fn1,fn2...)
    当单击jq对象对应的组件后，会执行fn1，第二次点击会执行fn2...

注意：1.9版本删除了该方法，使用JQuery Migrate插件可以恢复此功能
```

### 30.8 插件：增强JQuery的功能

1. **```$.fn.extend(object)```**
```
$.fn.extend({
    方法名:function(){
        this：调用该方法的jq对象
    },
    方法名2...
})

增强通过JQuery获取的对象的功能
调用：
    jq对象.方法名
```
2. **```$.extend(object)```**
```
$.extend(object)

增强JQuery对象自身的功能 对$或JQuery对象增强，全局方法
调用：
    $.方法名
```

## 31 AJAX

+ Asynchronous Javascript And XML 异步的JavaScript 和 XML

### 31.1 异步和同步：客户端和服务器端相互通信的基础上

+ 同步：客户端必须等待服务器端的响应。在等待的期间客户端不能做其他操作
+ 异步：客户端不需要等待服务器端的响应。在服务器处理请求的过程中，客户端可以进行其他的操作

+ AJAX：无需重新加载整个网页的情况下，能够更新部分网页的技术。

### 32.2 实现方式

+ 原生的JS实现方式【了解，不用，可以看w3school的文档，859集】

+ JQuery实现方式

#### 32.2.1 ```$.ajax()```

```
function fun(){ //绑定的按钮的单击事件的函数

	$.ajax({
		url:"ajaxServlet",//请求路径
		
		type:"POST",//请求方式
		
		data:"username=a&age=1",//请求参数写法1
		data:{"username":"jack","age":23},//请求参数写法2，JSON，推荐
		
		success:function(data){
			data：定义一个形参，名字无所谓，可以接受返回值
		},//响应成功后的回调函数
		
		error:function(){
			...
		},//请求响应出现错误，会执行的回调函数
		
		dataType:"text"//设置接收到的相应数据的格式
	});
	
}
```

#### 32.2.2 ```$.get()```

```
$.get(url,[data],[callback],[type])
    参数：
        url：请求路径
        data：请求参数
        callback：回调函数
        type：响应结果的类型
```

#### 32.2.3 ```$.post()```

```
$.post(...)
```

## 32 JSON

+ JavaScript Object Notation	JavaScript对象表示法
+ json现在多用于存储和交换文本信息的语法
+ 进行数据的传输
+ JSON比XML更小、更快、更易解析

### 32.1 语法

#### 32.1.1 基本规则

+ 数据在名称/值对中：json数据是由键值对构成的
   + 键用引号引起来，也可以不使用引号
   + 值的取值类型
      1. 数字（整数或浮点数）
      2. 字符串（在双引号中）
      3. 逻辑值（true 或 false）
      4. 数组（在方括号中）
      5. 对象（在花括号中）
      6. null
+ 数据由逗号分隔：多个键值对由逗号分隔
+ 花括号保存对象：使用{}定义json格式
+ 方括号保存数组：[]

#### 32.1.2 获取数据

```
json对象.键名

json对象["键名"]

数组对象[索引]
```
遍历：
```
for in 循环:
for(var key in person){
    这样获取的key是字符串，所以取值要用
    person[key];
}

数组循环：
for(var i =0; i<ps.length; i++){
    ...
}
```
### 33.2 JSON数据和Java对象的相互转换

+ JSON解析器：
常见的解析器：Jsonlib, Gson, Fastjson, jackson

#### 33.2.1 JSON转为Java对象

1. 导入Jackson的相关jar包
2. 创建Jackson核心对象```ObjectMapper```
3. 调用ObjectMapper的相关方法进行转换
```
readValue(json字符串数据,Class)
```

#### 33.2.2 Java对象转为JSON

1. 导入Jackson的相关jar包
2. 创建Jackson核心对象ObjectMapper
3. 调用ObjectMapper的相关方法进行转换
+ 转换方法
```
writeValue(参数1, obj)：
    参数1：
        File：将obj对象转换为JSON字符串，并保存到指定的文件中
        Writer：将obj对象转换为JSON字符串，并将json数据填充到字符输出流中
        OutputStream：将obj对象转换为JSON字符串，并将JSON数据填充到字节输出流中

writeValueAsString(obj)：将对象转为JSON字符串
```

+ 注解：加在类的成员变量上或get方法上。
```
@JsonIgnore：排除属性。

@JsonFormat：属性值的格式化。传入属性pattern
```
+ 复杂java对象转换
```
List：数组
Map：对象格式一致，键值对
```

### 33.3 案例

检验用户名是否存在

+ 服务器响应的数据，在客户端使用时，要想当做json数据格式使用
   1. ```$.get(type)```：将最后一个参数type指定为“json”
   2. 在服务器端设置MIME类型
      ```response.setContentType("application/json;charset=utf-8");```

## 33 Redis

+ redis是一款高性能的NoSQL系列的非关系型数据库。可以用来做缓存

### 33.2 命令操作

#### 33.2.1 redis的数据结构：

+ redis存储的是：key，value格式的数据，其中key都是字符串，value有5种不同的数据结构
+ value的数据结构：
   1. 字符串类型string
   2. 哈希类型hash：map格式
   3. 列表类型list：linkedlist格式。支持重复元素
   4. 集合类型set：不允许重复元素
   5. 有序集合类型sortedset：不允许重复元素，且元素有顺序

#### 33.2.2. 字符串类型string

```
存储：
	set key value

获取：
	get key

删除：
	del key
```

#### 33.2.3. 哈希类型hash

```
存储：
	hset key field value

获取：
	hget key field：获取指定的field对应的值
	hgetall key：获取所有的field和value

删除：
	hdel key field
```

#### 33.2.4. 列表类型list

可以添加一个元素到列表的头部（左边）或者尾部（右边）
```
添加：
	lpush key value：将元素加入列表左边【value可以直接写多个，空格隔开】
	rpush key value：将元素加入列表右边

获取：
    lrange key start end：范围获取，获取所有：0 -1

删除：
    lpop key：删除列表最左边的元素，并将元素返回
    rpop key：删除列表最右边的元素，并将元素返回
```

#### 33.2.5. 集合类型set：不允许重复元素

```
存储：
	sadd key value【value可以直接写多个，空格隔开】

获取：
	smembers key：获取set集合中所有元素

删除：
	srem key value：删除set集合中的某个元素
```

#### 33.2.6. 有序集合类型sortedset：不允许重复元素，且元素有顺序

```
存储：
	zadd key score value：会按照score从小到大排序

获取：
	zrange key start end：要显示分数，后面加withscores

删除：
	zrem key value
```

#### 33.2.7. 通用命令

```
keys *：查询所有的键【正则表达式】

type key：获取键对应的value的类型

del key：删除指定的key value
```

### 33.3 持久化

+ redis是一个内存数据库，当redis服务器重启，数据会丢失，我们可以将redis内存中的数据持久化保存到硬盘的文件中
+ redis持久化机制：RDB和AOF

#### 33.3.1 RDB

+ 默认方式，不需要进行配置，默认使用这种机制
+ 在一定的间隔时间内，检测key的变化情况，然后持久化数据
+ 编辑redis.windows.conf进行配置。
  save 900 1那里，表示900秒内有1条k以上的key更改就会进行持久化存储
+ 启动的时候必须要用命令行，redis-server.exe redis.windows.conf

#### 33.3.2 AOF

+ 日志记录的方式，可以记录每一条命令的操作。每一条命令操作后，持久化数据，对性能影响较大

1. 编辑edis.windows.conf文件。
   appendonly改成yes
   然后
```
#appendsysnc always：每一次操作都进行持久化
appendsysnc everysec：每隔一秒进行一次持久化
#appendsysnc no：不进行持久化
```
2. 命令行指定配置文件打开

### 33.4 使用Java客户端操作redis：Jedis

+ Jedis：一款java操作redis数据库的工具

#### 33.4.1 使用步骤

1. 下载Jedis的jar包
2. 使用：
```
1. 获取连接
Jedis jedis = new Jedis("localhost",6379);//空参默认localhost：6379

2. 操作
jedis.set("key","value");【jedis的方法名和redis的命令一样】

3. 关闭连接
jedis.close();
```

```
setex(key,seconds,value)方法：把key：value存入redis，seconds秒后自动删除掉
```

#### 33.4.2 jedis连接池：JedisPool

使用：
1. 创建JedisPool连接池对象，可以空参，也可以把创建配置对象传入
2. 调用方法```getResource()```获取Jedis连接

创建配置对象：
```
JedisPoolConfig config = new JedisPoolConfig();
config.setXxx(n);
```

#### 33.4.3 缓存案例

先查redis里有没有，没有再去数据库查，查到后放入redis里
清除缓存的话：在数据库增删改的时候，删除redis里的对应数据

## 34 Maven

+ pom：项目对象模型Project Object Model

### 34.1 下载安装配环境变量

MAVEN_HOME
PATH  MAVEN_HOME \bin

```mvn -v```查看是否安装成功

### 34.2 文件

配置：conf/settings.xml
里面可以配置本地仓库的位置。在注释里，复制出来就行。

远程仓库【私服】

### 34.3 maven标准目录结构

src/main/java	核心代码部分
src/main/resources	配置文件部分
src/test/java	测试代码部分
src/test/resources	测试配置文件
src/main/webapp	web项目的页面资源，js，css，图片等等

+ cmd里面。cd 路径后要再敲一个盘符

### 34.4 maven命令

mvn clean 删除编译的东西，因为每个人的环境都不一样，一般拿到别人项目先clean
mvn complie：编译main下的代码
mvn test：编译main和test下的代码
mvn package：编译main和test下的代码，并打包，打成什么包在pom.xml里设置
mvn install：编译，打包，并放在本地仓库

发布：
mvn deploy 需要一些配置

### 34.9 jar包冲突

```
在dependency里写
<scope>provided</scope>
```
表示只在编译测试过程中起作用，test表示只在测试阶段起作用
web工程，这里导入的servlet包和tomcat软件里的包冲突了

### 34.12 数据库

scope的配置
test：junit
provided：servlet，jsp【不会被打包，已提供了的意思】
runtime：JDBC