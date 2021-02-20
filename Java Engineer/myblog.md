myblog笔记


DispatchServlet 配置
Spring Boot 如何处理静态 web 资源
消息转换器 HttpMessageConverter

wget https://labfile.oss.aliyuncs.com/courses/1367/lou-springboot-03.zip
unzip lou-springboot-03.zip
cd lou-springboot

# 出师未捷身先死

reading maven projects

reading xxx/pom.xml





```
server.port=8082
server.servlet.context-path=/shiyanlou/
```

```
spring.resources.static-locations=classpath:/shiyanlou/
```

```
spring.resources.static-locations=classpath:/shiyanlou/,classpath:/static/
```



spring.thymeleaf.cache=false



配置含义注释：

- **spring.servlet.multipart.enabled**

  是否支持 multipart 上传文件，默认支持

- **spring.servlet.multipart.file-size-threshold**

  文件大小阈值，当大于这个阈值时将写入到磁盘，否则存在内存中，（默认值 0 ，一般情况下不用特意修改）

- **spring.servlet.multipart.location**

  上传文件的临时目录

- **spring.servlet.multipart.max-file-size**

  最大支持文件大小，默认 1 M ，该值可适当的调整

- **spring.servlet.multipart.max-request-size**

  最大支持请求大小，默认 10 M

- **spring.servlet.multipart.resolve-lazily**

  判断是否要延迟解析文件（相当于懒加载，一般情况下不用特意修改），默认 false