# Tomcat源码阅读

https://www.cnblogs.com/tanshaoshenghao/p/10932306.html

## 下载和环境

+ 官网下载的Tomcat7。进入官网后左边的目录中选择Tomcat7，下拉到页面的最下方，就可以看见源码的下载连接了。

+ 打开idea，open源码目录
+ 配置JDK与sources文件夹

## startup分析

rem是注释
@echo是打印指令

+ 总结: startup.bat文件实际上就做了一件事情: 启动catalina.bat。

```"%EXECUTABLE%" start %CMD_LINE_ARGS%```

## catalina.bat

设置当前目录为CATALINA_HOME，确保有catalina.bat后，赋值给CATALINA_BASE

执行setenv.bat和setclasspath.bat，获取CLASSPATH

把CLASSPATH和CATALINA_HOME拼接，定位到bootstrap.jar文件【启动tomcat的环境】

配置一大堆环境

设置tomcat的启动类为org.apache.catalina.startup.Bootstrap

set ACTION=start

**总结: catalina.bat最终执行了Bootstrap类中的main方法.**

ps: 分析完整个catalina.bat我们发现我们可以通过设定不同的参数让tomcat以不同的方式运行. 在ide中我们是可以选择debug等模式启动tomcat的, 也可以为其配置参数, 在catalina.bat中我们看到了启动tomcat背后的运作流程.

# Tomcat启动流程分析
![img](https://www.cnblogs.com/images/cnblogs_com/tanshaoshenghao/1486568/o_44.png)

![img](https://www.cnblogs.com/images/cnblogs_com/tanshaoshenghao/1486568/o_55.png)





# 黑马Tomcat专题

## 源码安装和目录结构

官网下载64位windows安装包，解压即可。

目录结构

bin：可执行文件，startup和shutdown

config：配置文件

logging日志配置

server服务器的配置

tomcat-users用户和角色配置

web.xml部署的应用

work：编译完的jsp字节码



## 源码下载和运行

1. 下载
2. 运行：
3. 解压zip
4. 创建目录home，把conf、webapp移入
5. 创建一个pom.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
 
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.apache.tomcat</groupId>
    <artifactId>Tomcat8.5</artifactId>
    <name>Tomcat8.5</name>
    <version>8.5</version>
 
    <build>
        <finalName>Tomcat8.5</finalName>
        <sourceDirectory>java</sourceDirectory>
        <testSourceDirectory>test</testSourceDirectory>
        <resources>
            <resource>
                <directory>java</directory>
            </resource>
        </resources>
        <testResources>
           <testResource>
                <directory>test</directory>
           </testResource>
        </testResources>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
 
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.easymock</groupId>
            <artifactId>easymock</artifactId>
            <version>3.4</version>
        </dependency>
        <dependency>
            <groupId>ant</groupId>
            <artifactId>ant</artifactId>
            <version>1.7.0</version>
        </dependency>
        <dependency>
            <groupId>wsdl4j</groupId>
            <artifactId>wsdl4j</artifactId>
            <version>1.6.2</version>
        </dependency>
        <dependency>
            <groupId>javax.xml</groupId>
            <artifactId>jaxrpc</artifactId>
            <version>1.1</version>
        </dependency>
        <dependency>
            <groupId>org.eclipse.jdt.core.compiler</groupId>
            <artifactId>ecj</artifactId>
            <version>4.5.1</version>
        </dependency>
       
    </dependencies>
</project>

```



配启动类

设置Add application + application 

就叫BootStrap就好

Main class设置为org.apache.catalina.startup.Bootstrap

添加VM options 

```
-Dcatalina.home=D：...
-Dcatalina.base=catalina-home
、、-Djava.endorsed.dirs=catalina-home/endorsed
、、-Djava.io.tmpdir=catalina-home/temp
-Djava.util.logging.manager
=org.apache.juli.ClassLoaderLogManager
-Djava.util.logging.config.file
=catalina-home/conf/logging.properties
```



https://www.cnblogs.com/grasp/p/10061577.html













# 鲁班学院

## Tomcat底层架构

Tomcat一个Servlet容器

RequestFacade
门面模式（包工头）
RequestFacade --- 门面
	Request

代理模式1对1
门面模式1对多

Context --- 应用 --- Servlet
Host --- 虚拟主机 --- Context
Engine --- Host

Wrapper：一个具体的Servlet的类的实例的集合
Context是Wrapper的集合

上面这4个节点【接口】下都有管道，管道下有阀门
Pipeline
Valve
每个管道的最后一个阀门：Tomcat实现，把Request交给下一层

FilterChain



数据：
操作系统实现TCP协议
HTTP协议：Tomcat

socket：对操作系统tcp_connect()的封装，一个API，建立tcp连接

