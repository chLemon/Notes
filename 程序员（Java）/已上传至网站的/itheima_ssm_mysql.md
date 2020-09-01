黑马ssm企业权限管理系统项目
https://www.bilibili.com/video/BV1mE411X7yp?p=299


# product表的创建：
```
create database ssm;
use ssm;

CREATE TABLE product
(
    id int PRIMARY KEY auto_increment,
    productNum VARCHAR(50) UNIQUE NOT NULL,
    productName VARCHAR(50),
    cityName VARCHAR(50),
    DepartureTime timestamp,
    productPrice double,
    productDesc VARCHAR(500),
    productStatus INT
);
```
# member表的创建

```
CREATE TABLE member(
       id int PRIMARY KEY auto_increment,
       NAME VARCHAR(20),
       nickname VARCHAR(20),
       phoneNum VARCHAR(20),
       email VARCHAR(50)
);
```

# traveller表的创建

```
CREATE TABLE traveller(
      id int PRIMARY KEY auto_increment,
      NAME VARCHAR(20),
      sex VARCHAR(20),
      phoneNum VARCHAR(20),
      credentialsType INT,
      credentialsNum VARCHAR(50),
      travellerType INT
);

```

# orders表的创建

```
CREATE TABLE orders(
   id int PRIMARY KEY auto_increment,
   orderNum VARCHAR(50) NOT NULL UNIQUE,
   orderTime TIMESTAMP,
   peopleCount INT,
   orderDesc VARCHAR(500),
   payType INT,
   orderStatus INT,
   productId int,
   memberId int,
   constraint order_product FOREIGN KEY (productId) REFERENCES product(id),
   constraint order_member FOREIGN KEY (memberId) REFERENCES member(id)
);

```

# order_traveller表的创建

```
CREATE TABLE order_traveller(
    orderId INT,
    travellerId INT,
    PRIMARY KEY (orderId,travellerId),
    FOREIGN KEY (orderId) REFERENCES orders(id),
    FOREIGN KEY (travellerId) REFERENCES traveller(id)
);
```

# 数据插入顺序

product --> member --> traveller --> orders --> order_traveller

# product数据

```
insert into PRODUCT (id, productnum, productname, cityname, departuretime, productprice,
                     productdesc, productstatus)
values (1,'itcast-002', '北京三日游', '北京', '20181010101000', 1200, '不错的旅行', 1);

insert into PRODUCT (id, productnum, productname, cityname, departuretime, productprice,
                     productdesc, productstatus)
values (2, 'itcast-003', '上海五日游', '上海', '20180425143000', 1800, '魔都我来了', 0);

insert into PRODUCT (id, productnum, productname, cityname, departuretime, productprice,
                     productdesc, productstatus)
values (3, 'itcast-001', '北京三日游', '北京', '20181010101000', 1200, '不错的旅行', 1);
```

# order数据

```
insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('1', '12345', 20180302120000, 2, '没什么', 0, 1, '1','1');

insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('2', '54321', 20180302120000, 2, '没什么', 0, 1, '1','1');

insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('3', '67890', 20180302120000, 2, '没什么', 0, 1, '2','1');

insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('4', '98765', 20180302120000, 2, '没什么', 0, 1, '2', '1');

insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('5', '11111',20180302120000, 2, '没什么', 0, 1, '2','1');

insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('6', '22222', 20180302120000, 2, '没什么', 0, 1, '2','1');

insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('7', '33333', 20180302120000, 2, '没什么', 0, 1, '3','1');

insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('8', '44444', 20180302120000, 2, '没什么', 0, 1, '3','1');

insert into ORDERS (id, ordernum, ordertime, peoplecount, orderdesc, paytype, orderstatus,productid, memberid) values ('9', '55555', 20180302120000, 2, '没什么', 0, 1, '3','1');
```

# member数据
```
insert into MEMBER (id, name, nickname, phonenum, email) values ('1', '张三', '小三', '18888888888', 'zs@163.com');
```

# traveller数据

```
insert into TRAVELLER (id, name, sex, phonenum, credentialstype, credentialsnum, travellertype) values ('1', '张龙', '男', '13333333333', 0, '123456789009876543', 0);

insert into TRAVELLER (id, name, sex, phonenum, credentialstype, credentialsnum, travellertype) values ('2', '张小龙', '男', '15555555555', 0,'987654321123456789', 1);
```

# order_traveller数据

```
insert into ORDER_TRAVELLER (orderid, travellerid)
values ('1', '1');

insert into ORDER_TRAVELLER (orderid, travellerid)
values ('3', '1');

insert into ORDER_TRAVELLER (orderid, travellerid)
values ('9', '2');

insert into ORDER_TRAVELLER (orderid, travellerid)
values ('7', '2');

insert into ORDER_TRAVELLER (orderid, travellerid)
values ('2', '1');

insert into ORDER_TRAVELLER (orderid, travellerid)
values ('6', '2');

insert into ORDER_TRAVELLER (orderid, travellerid)
values ('4', '1');

insert into ORDER_TRAVELLER (orderid, travellerid)
values ('8', '2');

insert into ORDER_TRAVELLER (orderid, travellerid)
values ('5', '2');
```

+ 主键可以有联合主键
+ 外键的两个列，类型要相同，长度要相等

# 类型转换

# PageHelper



# SSM权限操作

# users表的创建

```
CREATE TABLE users(
    id int PRIMARY KEY auto_increment,
    email VARCHAR(50) UNIQUE NOT NULL,
    username VARCHAR(50),
    PASSWORD VARCHAR(80),
    phoneNum VARCHAR(20),
    STATUS INT
)
```

# role表的创建

```
CREATE TABLE role(
    id int PRIMARY KEY auto_increment,
    roleName VARCHAR(50) ,
    roleDesc VARCHAR(50)
)
```

# permission表的创建

```
CREATE TABLE permission(
    id int PRIMARY KEY auto_increment,
    permissionName VARCHAR(50) ,
    url VARCHAR(50)
)
```

# users_role表的创建

```
CREATE TABLE users_role(
    userId int,
    roleId int,
    PRIMARY KEY(userId,roleId),
    FOREIGN KEY (userId) REFERENCES users(id),
    FOREIGN KEY (roleId) REFERENCES role(id)
)
```

# role_permission表的创建

```
CREATE TABLE role_permission(
    permissionId int,
    roleId int,
    PRIMARY KEY(permissionId,roleId),
    FOREIGN KEY (permissionId) REFERENCES permission(id),
    FOREIGN KEY (roleId) REFERENCES role(id)
)
```

# users表数据的添加

此处的几条数据都是我编的

```
insert into users values(1,"12@chlemon.cn","user","user","138",1);

insert into users values(2,"34@chlemon.cn","admin","admin","130",1);

insert into users values(3,"56@chlemon.cn","cannot","cannot","153",0);
```

# role表数据的添加

```
insert into role values(1,"ADMIN","管理员");

insert into role values(2,"USER","用户");
```

# users_role表数据添加

```
insert into users_role values (1,1);
insert into users_role values (1,2);
insert into users_role values (2,1);
insert into users_role values (3,2);
```

+ 这里注意两个坑：login.jsp里的form的action记得加.do
+ 另一个是：spring-security.xml里，配置加密方式 那行注释下面的代码删掉

# permission表数据添加

```
insert into permission values (1,"user.findAll","/user/findAll.do")
insert into permission values (2,"member.findAll","/member/findAll.do")
insert into permission values (3,"role.findAll","/role/findAll.do")
```

# role_permission表数据添加

```
insert into role_permission values (1,1)
insert into role_permission values (2,1)
insert into role_permission values (3,1)
insert into role_permission values (1,2)
```

+ user-show页面需要更改：146行开始改成：

```
<c:forEach items="${user.roles}" var="role" varStatus="vs">
    <tr data-tt-id="${vs.index+1}" data-tt-parent-id="0">
        <td>${role.roleName }</td>
        <td>${role.roleDesc }</td>
    </tr>
        <c:forEach items="${role.permissions}" var="permission">
            <tr data-tt-id="1-1" data-tt-parent-id="${vs.index+1}">
                <td>${permission.permissionName}</td>
                <td>${permission.url}</td>
            </tr>
        </c:forEach>
</c:forEach>
```



