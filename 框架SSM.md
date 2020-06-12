# Mybatis
第一天：mybatis入门
1. 概述
2. 环境搭建
3. 入门案例
4. 自定义mybatis框架（了解细节）

第二天：基本使用
1. 单表crud操作
2. 参数和返回值设置
3. dao编写
4. 配置细节：几个标签的使用

第三天：深入和多表
1. 连接池
2. 事务控制及设计的方式
3. 多表查询

第四天：缓存和注解开发
1. 加载时机
2. 一级缓存和二级缓存
3. 注解开发

## 第一天
1. 什么是框架？
	它是我们软件开发中的一套解决方案，不同的框架解决的是不同的问题。
	使用框架的好处：
		框架封装了很多的细节，使开发者可以使用极简的方式实现功能。大大提高开发效率。

2. 三层架构
	表现层：
		用于展示数据：SpringMVC
	业务层：
		处理业务需求
	持久层：
		和数据库交互：Mybatis
	Spring涉及到全部三层
3. 持久层技术解决方案
	JDBC技术：
		Connection
		PreparedStatement
		ResultSet
	Spring的JdbcTemplate：
		Spring中对jdbc的简单封装
	Apache的DBUtils：
		对jdbc的简单封装
	
	以上这些都不是框架，JDBC是规范，其余两个都只是工具类。

4. mybatis的概述
	mybatis是一个持久层框架，用java编写的。
	使开发者只关注sql语句本身。
	使用了ORM思想实现了结果集的封装
	
	ORM：Object Relational Mapping 对象关系映射
	简单的说，就是把数据库表和实体类以及实体类的属性对应起来，让我们可以操作实体类就实现操作数据库表。
	
5. mybatis的入门案例

环境搭建：
1. 创建maven工程```<packaging>```
2. 数据库初始化
3. maven依赖导入：
   1. mybatis官网，导入mybatis的依赖
   2. mysql的
   3. log4j
   4. junit
4. 建实体类，记得实现Serializable接口
5. 在resource下，创建xml文件，SqlMapConfig.xml。【提供了约束，需要导入】
6. 主配置文件：
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!-- mybatis的主配置文件 -->
<configuration>
    <!-- 配置环境 -->
    <environments default="mysql">
        <!-- 配置mysql的环境，上面的default和下面的id必须相同-->
        <environment id="mysql">
            <!-- 配置事务的类型-->
            <transactionManager type="JDBC"></transactionManager>
            <!-- 配置数据源（连接池） -->
            <dataSource type="POOLED">
                <!-- 配置连接数据库的4个基本信息 -->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/eesy_mybatis"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>

    <!-- 指定映射配置文件的位置，映射配置文件指的是每个dao独立的配置文件 -->
    <mappers>
        <mapper resource="com/itheima/dao/IUserDao.xml"/>
    </mappers>
</configuration>
```
7. 在resource下创建文件"com/itheima/dao/IUserDao.xml"。映射配置文件。
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.itheima.dao.IUserDao">
    <!--配置查询所有，上面这个namespace必须是dao接口的全限定类名，下面这个id必须是接口的方法名-->
    <select id="findAll" resultType="com.itheima.domain.User">
        select * from user
    </select>
</mapper>
```
8. Mybatis里一般管Dao叫Mapper
9. 满足：
   1. 映射配置文件与dao接口的包结构相同
   2. namespace与dao接口全限定类名相同
   3. id与dao的方法名相同
   就可以不用写dao的实现类

入门案例：
1. 直接拷贝log4j的配置文件

```
        //1.读取配置文件
        InputStream in = Resources.getResourceAsStream("SqlMapConfig.xml");
        //2.创建SqlSessionFactory工厂
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        SqlSessionFactory factory = builder.build(in);
        //3.使用工厂生产SqlSession对象
        SqlSession session = factory.openSession();
        //4.使用SqlSession创建Dao接口的代理对象
        IUserDao userDao = session.getMapper(IUserDao.class);
        //5.使用代理对象执行方法
        List<User> users = userDao.findAll();
        for(User user : users){
            System.out.println(user);
        }
        //6.释放资源
        session.close();
        in.close();

```
入门案例：
1. 读配置
2. 创建工厂：SqlSessionFactory
3. 创建SqlSession
4. 创建代理对象
5. 调用方法
6. 释放资源

注解配置：
在主配置里更改mappers：
```
    <!-- 指定映射配置文件的位置，映射配置文件指的是每个dao独立的配置文件
        如果是用注解来配置的话，此处应该使用class属性指定被注解的dao全限定类名
    -->
    <mappers>
        <mapper class="com.itheima.dao.IUserDao"/>
    </mappers>
```
然后在接口的方法上面加注解：
```
@Select("select * from user")
```

映射配置文件就可以删了



也可以写实现类，SqlSession有个方法，select.selectList，有一堆重载，传入一个statement，sql语句执行对象，这里传的是 接口全限定类名.方法名
也就是原来写在映射配置文件里的namespace.id



写路径的问题：
相对路径：现在在src目录下，但是之后编译完就不在了
绝对路径：不太好

所以一般这两个都不用，
第一个：类加载器
第二个：ServletContext的getRealPath



selectList方法分析：
执行这个方法，需要1. 数据库的连接信息 2. 映射信息
映射信息包含2部分：sql语句和实体类的全限定类名
映射信息就组合起来定义成一个对象，到时候放在一个map里存储起来，key就是用namespace.id


代理对象创建部分：
Proxy.newProxyInstance传入类加载器，存放了代理对象实现的接口的数组，和如何代理的方法

如何代理是一个InvocationHandler的接口，写一个实现类实现了selectList方法


自定义Mybatis：

## 第二天
1. 回顾mybatis的自定义再分析和环境搭建+完善基于注解的mybatis
2. mybatis的crud（基于代理dao的方法）
3. mybatis中的参数深入及结果集的深入
4. 基于传统dao的方式——了解
5. 配置（主配置文件）
   properties标签
   typeAliases标签
   mappers标签

通过注解拿到要封装的实体类
字节码对象，拿到方法数组，看方法上有没有select注解，然后拿到注解，然后拿方法的返回值，带泛型信息的，强转为参数化的类型，然后拿参数化类型中的实际参数（即参数化类型里的泛型），拿到实体类，强转class，拿到名称


