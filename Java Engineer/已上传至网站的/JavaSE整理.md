# JavaSE

## 1 基础知识与JDK安装

### 1.1 计算机基础知识

#### 1.1.1 字节

​	bit：位
​	Byte：字节，数据存储的最小单位
​		**1 Byte = 8 bit**

#### 1.1.2 常用DOS命令

```
1. 切换盘符：
                                                        盘符名称：
盘符名称不区分大小写
2. 进入文件夹：
注意：在win10的cmd里，Tab补全的时候连按可以切换
                                                       cd 文件夹名称
3. 进入多级文件夹：
                                                   cd 文件夹1\文件夹2\文件夹3
4. 返回上一级：
                                                          cd ..
5. 直接返回根路径：
                                                           cd \
6. 查看当前目录下的文件：
                                                           dir
7. 清屏：
                                                           cls
8. 退出cmd：
                                                           exit
```

+ 在cmd里运行.exe文件的时候可以省略后缀

### 1.2 Java安装

#### 1.2.1 Java虚拟机——JVM

Java语言有跨平台特性
java虚拟机（Java Virtual Machine）本身不具备跨平台功能，每个操作系统下都有不同版本的虚拟机

#### 1.2.2 JAVA_HOME环境变量的配置

+ JAVA_HOME
+ Path
%JAVA_HOME%\bin
【这里他安装的时候去掉了最下面的独立的JRE，加环境变量的时候也没加%JAVA_HOME%\jre\bin】
```CLASSPATH = .;%Java_Home%\bin;%Java_Home%\lib\dt.jar;%Java_Home%\lib\tools.jar```

## 2 HelloWorld

### 2.1 程序开发步骤说明

编写、编译、运行
javac.exe：编译器
java.exe：解释器

#### 2.1.1 编译Java源文件

```
javac HelloWorld.java
```

### 2.1.2 运行Java程序

```
java HelloWorld
```

### 2.2 一些说明

+ 编译和运行是两回事

+ main方法：程序执行的起点

### 2.3 添加注释 comment

```
//单行注释
/*
多行注释
*/
```

### 2.4 关键字 keywords

+ 完全小写的单词
+ 在IDE中有特殊颜色

### 2.5 标识符

类名、方法名、变量名等
+ 包含字母、数字、$、\_
+ 不能以数字开头
+ 不能是关键字
  + 类名：大驼峰
  + 变量和方法：小驼峰

## 3 数据类型

注意：

+ 字符类型两个单引号中间不能什么都不写
+ 不能直接println(null)

### 3.1 数据类型分类

基本数据类型：8个
 + 整数型 byte short int long
 + 浮点型 float double
 + 字符型 char
 + 布尔型 boolean：true、false

### 3.2 定义变量

```
数据类型 变量名;
数据类型 变量名 = 数据值;
long num = 200L; //记得写这个L
```

### 3.3 注意

1. 字符串是引用类型
2. 浮点数可能只是一个近似值
3. 数据范围与字节数不一定相关，例如float（4字节）数据范围比long（8字节）更广泛
4. 浮点数默认double，如果要用float，在后面加F；整数默认int，如果用long，在后面加L【F、L的大小写均可以，推荐大写】

### 3.4 数据类型转换

#### 3.4.1 自动转换（隐式）

转换规则：**数据范围从小到大。**

#### 3.4.2 强制转换（显示）
```
int num = (int) 100L;
```
#### 3.4.3 注意

1. 不推荐使用，因为可能发生精度损失、数据溢出。
2. byte/short/char在进行数学运算的时候，都会被提升成int类型然后再计算！
3. boolean类型不能发生数据类型转换

### 3.5 ASCII编码表
48 -- '0'
65 -- 'A'
97 -- 'a'

## 4 运算符

### 4.1 算数运算符

```
+
-
*
/【整数除法是地板除】
%
++
--
```

1. 运算中有不同类型的数据，会先变成数据范围大的类型，然后再计算。
2. “+”可以用于字符串拼接
3. ++num先加后用，num++先用后加

### 4.2 赋值运算符

```
=
+=
-=
*=
/=
%=
```

注意：复合赋值运算符会有隐含的强制类型转换
```
short a = 5;
a += 5;  //a还是short
```

### 4.3 比较运算符

```
==
<
>
<=
>=
!=
```

### 4.4 逻辑运算符

短路运算符：如果根据左边已经可以判断得到的最终结果，那么右边的代码将不再执行。
```
&&
||
!
```

### 4.5 三元运算符

```
数据类型 变量名称 = 条件判断 ？ 表达式A ：表达式B;
```
如果条件是true，把表达式A赋值给变量；如果是false，把表达式B赋值给变量。
```
int max = a > b ? a : b;
```

### 4.6 扩展知识点

1. 对于byte/short/char三种类型来说，如果右侧赋值的数值没有超过范围，那么javac编译器将会自动隐含地补上(byte)
2. 在给变量赋值的时候，如果右侧的表达式当中全都是常量，没有变量，那么编译器会直接把若干常量表达式计算得到结果。
    ```short a = 5 + 8;```
    编译完后字节码文件里相当于是
    ```short a = 13;```
这被称为**编译器的常量优化**。

## 5 流程控制

顺序、分支、循环

### 5.1 判断语句

```
if

if...else

if...else if...else
```

### 5.2 选择语句switch

+ 记得写    default：和        break;

+ switch小括号内**只能**是下列数据类型【2种字符和3种整数+枚举，没有long】
  基本数据类型：byte / short / char / int
  引用数据类型：String、enum

+ 注意case的穿透性

### 5.3 循环语句

#### 5.3.1 循环概述

初始化语句
条件判断
循环体
步进语句

#### 5.3.2 循环语句

```
for
while
do...while
```

#### 5.3.3 跳出循环

+ break
+ continue

#### 5.3.4 死循环

停不下来的死循环后写的语句无法访问，编译器会报错。

## 6 方法

+ 方法重载：

多个方法名称相同，参数不同【个数不同、类型不同、多类型顺序不同】，与返回值无关【同名的不同返回值的两个方法不能同时存在】


## 7 数组

### 7.1 数组的定义

```
int[] array = new int[300];
int[] array = new int[] {1,2,3};
int[] array = {1,2,3};
```

直接打印数组名称，得到的是数组对应的 内存地址**哈希值**。

**数组未赋值的有默认值：**

整数：0
浮点：0.0
字符：'\u0000'【不可见字符】
布尔：false
引用：null

### 7.2 内存

Java的内存划分为5个部分：
1. 栈（Stack）：存放的都是方法中的局部变量。方法的运行在栈里。
2. 堆（Heap）：凡是new出来的东西，都在堆当中。
堆内存里面的东西都有一个地址值：16进制
堆内存的数据，都有默认值，规则见上
3. 方法区（Method Area）：存储.class相关信息，包含方法的信息。
4. 本地方法栈（Native Method Stack）：与操作系统相关。
5. 寄存器（pc Register）：与CPU相关。

### 7.3 数组的长度和其他

+ 数组长度：

```
int l = array.length
```

+ 数组遍历：

`array.fori`会自动生成for循环

+ for循环里的变量可以不止一个，把握住初始化语句、条件判断、步进表达式三个关键

+ 数组作为方法参数，传进去的是数组地址

+ 数组作为返回值：
  `public static int[] method()`
  返回的也是地址

## 8 类

+ 导包：
import 包名称，类名称
对于和当前类属于同一个包的情况，可以省略导包语句不写

+ 进栈也叫压栈
  出栈也叫弹栈

+ 局部变量和成员变量：
局部变量：没有默认值，没赋值不能用，栈
成员变量：不指定，会有默认值，堆

+ 对于boolean，Get方法名字应该是isVariable

+ 构造方法注意事项：
1. 名称与类名一模一样
2. 没有返回值类型

### JavaBean
一个Java Bean，一个标准的类：
1. 所有成员变量都是用private
2. 所有成员变量都编写一对Getter/Setter【Alt+Insert，或者菜单栏Code--Generate】【shift多选，不知道ctrl行不行】
3. 编写一个无参数的构造方法   【Alt+Insert，或者菜单栏Code--Generate】Constructor
4. 编写一个全参数的构造方法  同上

## 9 API

### 概述

Application Programming Interface，应用程序编程接口

java.lang
lang：language

## 10 Scanner类

+ 什么是Scanner类：输入

### 10.1 引用类型使用步骤

1. 导包
只有java.lang包下的内容不需要导
2. 创建对象
new
3. 调用方法

### 10.2 Scanner使用步骤

```
import java.util.Scanner; //这句可以不用自己写，直接输入Scanner敲个回车就会自动导入
或者用Alt+Enter补全
...
Scanner sc = new Scanner(System.in);
int num = sc.nextInt();
String str = sc.next(); //记这个
```

即：
```
Scanner sc = new Scanner(System.in);
String str = sc.next();
```

### 10.3 匿名对象【了解】

只用一次的对象，就可以：
```
int num = new Scanner(System.in).nextInt();
```

## 11 Random类

### 11.1 Random使用步骤

```
import java.util.Random;
Random r = new Random();
r.nextInt(); //范围是int所有范围，包括正负
r.nextInt(n); //范围是[0,n)
```

## 12 ArrayList类

### 12.1 ArrayList使用步骤

```
ArrayList<E> //E：泛型
```
注意，泛型只能是引用类型
```
ArrayList<String> list = new ArrayList<>();
```
+ 注意事项：
对于ArrayList集合来说，直接打印得到的不是地址值，而是内容。如果内容是空，得到的是空的中括号：[]

### 12.2 常用方法和遍历

```
public boolean add(E e);
public E get(int index);
public E remove(int index);
public int size();
```

### 12.3 如何存储基本数据类型

用包装类，其中int -- Integer，char -- Character

## 13 字符串String

1. 程序中所有的双引号字符串，都是String类的对象，就算没有new，也照样是
2. 字符串不可变
3. 字符串可以共享使用
4. 效果上相当于char[]，但是原理上是byte[]

### 13.1 创建的常见方法

```
public String();   //创建一个空白字符串
public String(char[] array);  //根据字符数组的内容，创建相应的字符串
public String(byte[] array);  //根据字节数组的内容，创建相应的字符串
```

### 13.2 字符串常量池

位于堆中
**双引号直接写的字符串在常量池中**

### 13.3 ==运算符

对基本类型来说，进行的数值的比较
对引用类型来说，进行的**地址值**的比较

### 13.4 常用方法
#### 13.4.1 内容比较

```
public boolean equals(Object obj);//推荐把常量写在前面，如："abc".equals(str),变量可能会是null，.的时候会报错

public boolean equalsIgnoreCase(String str);//忽略大小写，进行内容比较
```
控制台输出exception信息可能会断开，红字中间夹杂着黑字

#### 13.4.2 获取相关的常用方法

```
public int length();获取字符串中的字符个数，字符串长度

public String concat(String str);将当前字符串和参数字符串拼接返回

public char charAt(int index);获取指定索引位置的字符

public int indexOf(String str);查找参数字符串在本字符串中首次出现的索引位置，如果没有返回-1
```

#### 13.4.3 截取方法

```
public String substring(int index); 截取从参数位置一直到字符串末尾，返回新字符串

public String substring(int begin, int end); 截取一段字符串，左闭右开
使用：
```

#### 13.4.4 字符串转换

```
public char[] toCharArray();将当前字符串拆分成字符数组作为返回值

public byte[] getBytes();获取当前字符串底层的字节数组

public String replace(CharSequence target, CharSequence replacement);将所有的target替换成replacement，返回替换后的结果【CharSequence是个接口，可以接受String】
```

#### 13.4.5 分割方法

```
public String[] split(String regex);按照参数的规则，将字符串切分成若干部分
```
注意，此处的regex是正则表达式，regular expression

#### 13.4.6 其他

```
public boolean endsWith(str);
```

#### 13.4.7 另外

```
'A'<=ch && ch<='Z'     //判断一个字符是否是大写字母
```

## 14 static关键字

+ static修饰的变量：
属于类，所有对象公用。既可以通过对象名来调用，也可以直接通过类名称来调用，**推荐直接用类名称调用。**
  
+ static修饰的方法：
属于类，既可以通过对象名来调用，也可以直接通过类名称来调用，**推荐直接用类名称调用。**在当前类中可以直接用方法名称调用。

+ 静态 不能访问 非静态。因为在内存中是先有的静态

+ 静态不能使用this

**alt按住选变量可以一次性选全部**

+ 内存 方法区中专门有一块静态区

### 14.1 静态代码块

```
public class Person{
    static{
        //静态代码块内容
    }
}
```

**特点：**

+ 当第一次用到该类时，静态代码块执行唯一的一次。
+ 静态内容总是优先于非静态，静态代码块比构造方法先执行。

**典型用途：**

一次性地对静态成员变量进行赋值。

## 15 数组工具类Arrays

```java.util.Arrays```是一个数组相关的工具类，里面提供了大量静态方法，用来实现数组常见的操作。

```
public static String toString(数组);//将参数数组以默认格式变成字符串([元素1，元素2，...])

public static void sort(数组);//按照升序对数组元素进行排序。如果数组是自定义类型，那么这个类需要有Comparable或者Comparator接口的支持
```

IDEA使用技巧：
```array.length.fori```：正序循环
```array.length.forr```：倒叙循环
ctrl+f12，查看类中方法

## 16 数学工具类Math

```java.util.Math```类是数学相关的工具类

```
public static double abs(double num);获取绝对值，有多重重载int long float double

public static double ceil(double num);向上取值

public static double floor(double num);向下取整

public static long round(double num);四舍五入

Math.PI近似的圆周率
```

## 17 继承

继承主要解决的问题就是：共性抽取。

父类、子类

关键字：extends
```
public class Teacher extends Employee{
    //
}
```

### 17.1 访问成员变量

间接通过成员方法访问成员变量时，看方法在哪里，就优先用哪里。

### 17.2 重写，覆盖，覆写

Override：方法名称一样，参数列表也一样

Overload，重载，方法名称一样，参数列表不一样

注解（annotation）：@Override，用于检测是否正确实现重写

### 17.3 返回值与权限

+ 子类方法的返回值必须**小于等于**父类方法的返回值范围。

+ 子类方法的权限必须**大于等于**父类方法的权限修饰符

权限大小关系：
public>protected>(default)>private
default不是关键字，而是什么都不写，留空

### 17.4 其他

设计原则：
对于已经投入使用的类，尽量不要修改，推荐定义一个新的类，来重复利用其中的共性内容，并添加新的内容。

IDEA使用技巧：
子类里直接输入方法名，就会弹出父类方法，并添加重写注解

### 17.5 构造方法

继承关系中，构造方法的访问特点：
1. 子类构造方法中有一个默认的隐含的 super() 调用，父类的无参构造方法。
2. 可以通过super( args )调用父类重载构造方法。
3. super的父类构造方法调用必须是子类构造方法的第一个语句。且只能调用一个。

### 17.6 父类关键词：super；和this关键字

+ super关键字：
访问父类的成员变量，方法，构造方法

+ this关键字：
1. 可以访问本类的成员变量
2. 在本类的成员方法中访问另一个成员方法（可以不写）
3. 在构造方法中，调用另一个构造方法，也必须是构造方法的第一个语句。this()；而且super和this只能存在一个。

### 17.7 继承关系

Java语言是**单继承**的：一个类的**直接父类**只能有唯一一个
Java语言可以**多级继承**
java.lang.Object是所有类的父类

## 18 抽象

抽象方法：加上abstract关键字，然后去掉大括号，直接分号结束

```
public abstract void funtion();
```

+ **抽象方法所在的类必须是抽象类**，class前加上abstract即可

+ 抽象类中可以正常定义普通方法

抽象类和抽象方法的使用：
1. 不能直接new抽象类对象
2. 必须用一个子类来继承抽象类
3. 子类必须重写override（实现）抽象父类的所有抽象方法，除非子类也是个抽象类
4. 抽象类可以有构造方法，供子类中使用

*IDEA使用技巧：子类在刚写好类名后，会是有红线的，alt+enter，选择implement，可以直接出现需要override的抽象方法*

## 18 接口

接口就是一种公共的规范标准

接口是一种引用数据类型，最重要的内容就是其中的抽象方法

### 19.1 接口定义

```
public interface 接口名称{\
    //接口内容
}
```

接口编译生成的字节码依旧是.class

接口中可以包含：
1. 常量		java7
2. 抽象方法		java7
3. 默认方法		java8
4. 静态方法		java8
5. 私有方法		java9

IDEA使用技巧：创建新类的时候，用上下箭头就可以选择Kind：class、interface、enum、....

#### 19.1.1 接口中定义抽象方法

注意：
1. 接口中的抽象方法，修饰符必须是 public abstract
2. 这两个关键字可以选择性省略（可以全不写，也可以只写一个，都一样）

接口的使用：
1. 接口不能直接使用，必须有一个“实现类”来实现该接口
2. 接口的实现类必须override所有的抽象方法，除非实现类是抽象类

```
public class 实现类名称 implements 接口名称{
    //...
}
```

建议：实现类名写成 接口名Impl

#### 19.1.2 接口中定义默认方法

```
public default 返回值类型 方法名称（参数列表）{
    方法体
}
```

这里的必须是public，可以省略不写

默认方法可以解决**接口升级**的问题：接口后来又要添加新方法

1. 接口的默认方法，可以通过接口的实**现类对象，直接调用**
2. 接口的默认方法，也可以被接口实现类**进行覆盖重写**，也会被实现类继承

#### 19.1.3 接口中定义静态方法

```
public static 返回值类型 方法名称（参数列表）{
    方法体
}
```

这里的必须是public，可以省略不写

+ 注意：不能通过接口实现类的对象来调用接口当中的静态方法。
要**通过接口名称直接调用**其中的静态方法

#### 19.1.4 接口中定义私有方法

从Java 9 开始，接口内允许定义私有方法：

1. 普通私有方法：解决多个默认方法之间重复代码问题

```
private 返回值类型 方法名称（参数列表）{
    方法体
}
```

2. 静态私有方法：解决多个静态方法之间重复代码问题

```
private static 返回值类型 方法名称（参数列表）{
    方法体
}
```

#### 19.1.5 接口中定义常量

接口中也可以定义“成员变量”，但是必须使用**public static final**三个关键字修饰，从效果上看就是常量

+ 关键字可以省略
+ 接口中的常量必须进行赋值
+ 常量命名：全用大写字母，用下划线进行分隔

一旦使用final关键字修饰，说明不可改变

### 19.2 注意

1. 接口不能有**静态代码块**或者**构造方法**。
2. 一个类可以**实现多个接口**，用逗号隔开，implements 接口A，接口B，...，要覆盖重写所有的抽象方法
3. 如果实现类实现的多个接口中，存在**重复的抽象方法，那么只需要覆盖重写一次**
4. 如果实现类实现的多个接口中，存在**重复的默认方法，那么实现类必须对冲突的默认方法进行覆盖重写**
5. 一个类如果继承的父类中有默认方法，和接口当中的默认方法产生了冲突，**优先使用父类当中的方法**

### 19.3 类与接口的关系

1. 类与类之间是单继承的，直接父类只有一个
2. 类与接口之间是多实现的，一个类可以实现多个接口
3. 接口与接口之间是**多继承**的：如果父接口中的默认方法重复，那么子接口必须进行覆盖重写，而且带着default关键字

### 19.4 多态

一个子类对象既是父类，也是子类，一个对象多种形态

+ **注意：**
访问成员变量的两种方式：
1. 直接通过对象名称访问成员变量：看等号左边是谁，优先用谁，没有则向上找
2. 间接通过成员方法访问成员变量：看该方法属于谁，优先用谁，没有则向上找

举例：
父类有变量n=10，子类有变量n=20.
```
FatherClass fc = new SonClass();
fc.num //10
```
如果用方法获取n，如果是子类的方法，则n=20，如果是父类的方法，则n=10

+ 成员方法的访问：
看new的是谁，就优先用谁，没有则向上找
编译看左边，运行看右边

### 19.5 对象的向上转型

其实就是多态写法：

格式：
```
父类名称 对象名=new 子类名称();
Animal animal = new Cat();
```
含义：右侧创建一个子类对象，把它当做父类来看待使用

向上转型一定是安全的

**一旦向上转型为父类，那么就无法调用子类原本特有的内容**

### 19.6 对象的向下转型

其实是一个还原的动作

格式：
```
子类名称 对象名=（子类名称）父亲对象;
Cat cat = (Cat) animal;
```

将父类对象**还原**为原本的子类对象

注意事项：
1. 必须保证原本创建的时候就是子类对象
2. 如果创建的不是该子类，非要向下转型就会报错【编译不报错，运行会有ClassCastException】

### 19.7 instanceof

```
对象 instanceof 类名称
```
返回一个boolean值，判断前面的对象是不是后面类型的实例

接口可以直接像类名那样当参数传

## 20 final关键字

最终的，不可变的

常见四种用法：
1. 可以用来修饰一个类
2. 可以用来修饰一个方法
3. 可以用来修饰一个局部变量
4. 可以用来修饰一个成员变量

### 20.1 修饰一个类

```
public final class类{
    //...
}
```

含义：当前这个类不能有任何子类。（太监类）

### 20.2 修饰一个方法

```
修饰符 final 返回值类型 方法名（参数列表）{
    //方法体
}
```

含义：当前这个方法不能被覆盖重写。这个方法就是最终方法。

注意：
对于类、方法来说，abstract关键字和final关键字不能同时使用，自相矛盾。

### 20.3 修饰一个局部变量

含义：一旦使用final来修饰局部变量，那么这个变量就不能进行更改。一次赋值，终生不变。

基本类型：变量中的数据不可变
引用类型：变量中的**地址值**不可变

```
final int n = 100;
//或
final int n;
n = 100
```

### 20.4 修饰一个成员变量

1. 由于成员变量具有默认值，所以用了final之后必须手动赋值，否则会报错。
2. 对于final的成员变量，要么使用**直接赋值**，要么通过**构造方法赋值**。二选一。
用构造方法赋值时，必须保证**所有的构造方法都对该成员变量赋值**。

## 21 权限修饰符

||public >| protected >| (default) >| private|
|---|---|---|---|---|
|同一个类（我自己）|YES|YES|YES|YES|
|同一个包（我邻居）|YES|YES|YES|NO|
|不同包子类（我儿子）|YES|YES|NO|NO|
|不同包非子类（陌生人）|YES|NO|NO|NO|

+ default例子：
int a = 3;

java中只要不是严格同一个包，就需要导包。没有所谓的“子包”。

## 22 内部类

一个事物的内部包含另一个事物，就是一个类内部包含另一个类。
如：身体和心脏，汽车和发动机

分类：
1. 成员内部类
2. 局部内部内（包含匿名内部类）

### 22.1 成员内部类

成员内部类的定义格式：

```
修饰符 class 外部类名称{
    修饰符 class 成员内部类名称{
        //...
    }
    //...
}
```

+ 内用外，随意访问（包括private）；外用内，需要**内部类对象**。

+ 内部类的字节码文件：Body$Heart.class

#### 22.1.1 使用成员内部类

1. 间接方式：在外部类的方法中使用内部类，在main中【别的类】调用外部类的方法
2. 直接方式：
```
外部类名称.内部类名称 对象名 = new 外部类名称().new 内部类名称();
```

+ 同名变量的调用：
外部类名称.this.**外部类成员变量**
```
Outer.this.num
```

### 22.2 局部内部类

定义在方法内部的类。
只有当前所属的方法才能使用。

定义格式：
```
修饰符 class 外部类名称{
    修饰符 返回值类型 外部类方法名称（参数列表）{
        class 局部内部类名称{
            //...
        }
    }
}
```

#### 22.2.1 注意

类的权限修饰符：
1. 外部类：public、（default）
2. 成员内部类：public、protected、（default）、private
3. 局部内部类：什么都不能写

+ 局部内部类如果想访问所在方法的局部变量，那么这个局部变量必须是【有效final】的。
即，要么是final的，要么可以省略final，但是确实事实不变。

+ 原因：生命周期不一样。局部变量跟方法，在栈内存里，方法结束出栈局部变量就消失了。而内部类new出来的对象在堆中持续存在，直到回收。所以得让变量不变，才方便留一个副本在对象中。

### 22.3 匿名内部类（局部内部类）

如果接口的实现类（或者父类的子类）只需要使用**唯一的一次**
那么这种情况下就可以省略掉该类的定义，而改为使用匿名内部类

```
接口名称 对象名 = new 接口名称(){
    //覆盖重写所有抽象方法
};
//注意最后的分号
```

如果不写接口名称和对象名，就是一个匿名对象，只能调用唯一的一次

```
new 接口名称(){
    //覆盖重写所有抽象方法
}.method();
//注意最后的分号
```

### 22.4 其他

+ 类可以作为成员变量的类型
+ 接口也可以作为成员变量的类型
+ 接口还可以作为方法的参数

## 23 Object类

```java.lang.object```

无需导包，**所有类的父类**，它里面的方法所有子类都可以用

### 23.1 常用方法

```
protected Object clone();

Class<?> getClass();

boolean equals(Object obj);

String toString();
```

#### 23.2 toString方法

+ 默认返回的字符串是```对象的类名@地址值```

+ 直接打印对象的名字，其实就是调用对象的toString方法

IDEA中alt+insert中有toString方法的重写，可以打印对象的属性

#### 23.3 equals方法

内部源码：
```
return(this==obj);
```

==：基本数据类型，比较值；引用数据类型，比较地址值【hashCode的值】

+ 重写equals方法时要注意此处有多态，需要向下转型

该方法重写也可以直接通过alt+insert中equals() and hashCode()自动实现重写

## 24 Objects类

null是不能调用方法的，会抛出空指针异常

Objects类是一个空指针安全/容忍空指针的**工具类**

```
Objects.equals(Object a, Object b)
```

内部：
```
return (a==b)||(a!=null && a.equals(b))
```

如果a不为空比较内容，如果为空直接比较地址值

### 34.1 Objects.requireNonNull(T obj)

查看指定的引用对象不是null，是null抛出空指针异常，不是返回obj

有重载方法，再加个字符串，传递一句话

## 25 Date类

```java.util.Date```【注意一下，因为java.sql里也有个Date】

表示特定的瞬间，精确到毫秒

时间原点（0毫秒）：1970年1月1日 00:00:00

东八区要+8h

```
System.currentTimeMillis();//可以获取当前系统时间到时间原点的毫秒值
```

### 25.1 构造方法

空参数构造方法：获取系统当前的日期和时间
```
Date date = new Date();
```
带参数构造方法：Long date，传递毫秒值，把毫秒值转换为Date日期
```
Date date = new Date(0);//1970年1月1日 00：00:00
```

### 25.2 成员方法

```
long getTime();
```

在把当前日期转换为毫秒。相当于```System.currentTimeMillis()```

## 26 DateFormat类

```java.text.DateFormat```，该类是一个**抽象类**，有一个直接子类：```SimpleDateFormat```

作用：日期/时间 格式化 与 解析

### 26.1 成员方法

按照指定的模式，把Date日期，格式化为符合模式的字符串
```
String format(Date date)
```

把符合模式的字符串，解析为Date日期
该方法会throws ParseException，调用的时候需要处理
```
Date parse(String source)
```

## 27 SimpleDateFormat

构造方法：

```
SimpleDateFormat(String pattern)
```

用给定的**模式**和**默认语言环境**的日期格式符号构造SimpleDateFormat。

"yyyy-MM-dd HH:mm:ss"

模式中的**字母不能更改**，连接模式的符号可以改变

## 28 Calendar类

```java.util.Calendar```，替代掉了很多原Date类的方法，也是一个抽象类

+ **使用的时候用其静态方法getInstance获得一个通用对象**

### 28.1 常用方法

```
public int get(int field);返回给定日历字段的值

public void set(int field, int value);将给定的日历字段设置为给定值

public abstract void add(int field, int amount);根据日历的规则，为给定的日历字段，添加或减去指定的时间量

public Date getTime();返回一个表示此Calendar时间值的Date对象
```

+ 静态字段有：【```int field```】

```
YEAR/MONTH/DATE（DAY_OF_MONTH）/HOUR/MINUTE/SECOND

get(Calendar.YEAR);
```
+ 注意MONTH是0-11

+ set还有其他重载方法

+ amount可正可负

## 29 System类

```java.lang.System```

### 29.1 常用方法

```
public static long currentTimeMillis();返回以毫秒为单位的当前时间

public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length);将数组中指定的数据拷贝到另一个数组中，srcPos、destPos数组中的起始位置
```

例：
```
src=[1,2,3,4,5], dest=[6,7,8,9,10]
System.arraycopy(src, 0, dest, 0, 3);
dest//[1,2,3,9,10]
```

IDEA使用技巧：
选中多行后按tab：整体缩进，按shift+tab，整体去除缩进

## 30 StringBuilder类

字符串缓冲区，可以提高字符串的操作效率

String底层是一个final修饰的byte数组

StringBuilder底层也是一个数组，初始容量16，但是没有被final修饰

### 30.1 构造方法

```
StringBuilder();构造一个不带任何字符的字符串生成器

StringBuilder(String str);构造一个字符串生成器，并初始化为指定字符串内容
```

### 30.2 常用方法

```
public StringBuilder append(...);添加任意类型数据的字符串形式，并返回【当前对象自身】，该方法无需接收返回值

public String toString();将当前StringBuilder对象转换为String对象
```

## 31 包装类

基本类型有8个，包装类也有8个，都在```java.lang```下。

和基本类型名字不一致的有：

int -->  Integer
char --> Character

### 31.1 装箱与拆箱

#### 31.1.1 装箱

以Integer为例

##### 31.1.1.1 构造方法

```
Integer(int value);构造一个新分配的Integer对象，它表示指定的int值
该方法上会有横线，说明方法过时了

Integer(String s)；构造一个新分配的Integer对象，表示String参数所指示的int值，该字符串必须是int的字符串，否则会抛出异常NumberFormatException
```

##### 31.1.1.2 静态方法

```
static Integer valueOf(int i);返回一个表示指定的int值的Integer实例
static Integer valueOf(String str);返回保存指定String值的Integer对象
```

#### 31.1.2 拆箱

##### 31.1.2.1 成员方法

```
int intValue();以int类型返回该Integer的值
```

### 31.2 自动装箱和自动拆箱

自动装箱：直接把int类型的整数赋值给包装类

自动拆箱：直接赋值，或直接计算

## 32 基本类型与字符串类型的相互转换

### 32.1 基本类型转字符串

1. 基本类型+空字符串，```+“”```
2. 包装类的静态方法：```toString(参数)```，注意**该方法要带参数**
3. String类的静态方法```valueOf(参数)```

### 32.2 字符串转基本类型

包装类的静态方法```parseXXX(String str)```

## 33 泛型

+ E e：Element 元素
+ T t：Type 类型

在创建集合的时候不写```<E>```的时候，集合的类型就是Object

### 33.1 创建含有泛型的类

在类名后加上```<E>```

### 33.2 定义含有泛型的方法

```
修饰符 <泛型> 返回值类型 方法名(M m){//在参数列表处可以使用泛型
    //方法体
}
```

使用的时候直接传参，参数是什么类型，泛型就是什么类型

### 33.3 定义含有接口的泛型

定义接口：在接口名后加```<E>```即可

使用接口：
1. 定义实现类的时候直接确定泛型：```implements Interface<String>```
2. 定义类的时候不确定泛型，在创建对象的时候确定泛型：```implements List<E>```

### 33.4 泛型通配符

```<?>```

+ 泛型没有继承概念
+ 泛型通配符只能作为方法的参数使用

```
public void method(Collection<?> coll){//此时就无所谓传进来的到底是什么类型。之后可以用Object类的方法来处理
    //...
}
```

### 33.5 受限泛型

#### 33.5.1 泛型的上限

```? extends E```，代表使用的泛型只能是E类型的子类/本身

#### 33.5.2 泛型的下限

```? super E```，代表使用的泛型只能是E的父类/本身

## 34 Collection接口：集合

```Collection<E>```

集合和数组的区别：
1. 长度，前者可变，后者不可变
2. 集合不能存储基本类型，只能存对象

### 34.1 单列集合框架

| Collection接口                   | List接口                             |                                        |
| -------------------------------- | ------------------------------------ | -------------------------------------- |
| 定义的是所有单列集合中共性的方法 | 1. 有序的集合（存123取123,顺序一致） | Vector                                 |
| 没有带索引的方法                 | 2. 允许重复元素                      | ArrayList                              |
|                                  | 3. 有索引，可以用普通for循环遍历     | LinkedList                             |
|                                  |                                      |                                        |
|                                  | **Set接口**                          | TreeSet【无序】                        |
|                                  | 1. 不允许重复元素                    | HashSet【无序】                        |
|                                  | 2. 没有索引（不能用普通for循环遍历） | LinkedHashSet（继承自HashSet）【有序】 |

### 34.2 Collection常用功能

```java.util.Collection```单列集合的最顶层接口

```
public boolean add(E e);把给定的对象添加到当前集合中

public void clear();清空集合中所有的元素

public boolean remove(E e);从集合中删除给定对象

public boolean contains(E e);判断当前集合是否包含给定对象

public boolean isEmpty();判断当前集合是否为空

public int size();返回集合中元素的个数

public Object[] toArray();把集合中的元素存储到数组中	
```

### 34.3 Iterator接口：迭代器

Collection元素通用的获取方式

#### 34.3.1 常用方法

```
boolean hasNext();判断是否还有元素可以迭代

E next();返回迭代的下一个元素，没有元素后会抛出NoSuchElementException
```

Collection接口有个方法```Iterator<E> iterator()```，返回此collection的迭代器的实现类对象，泛型与集合相同

```
while(it.hasNext()){
    String e = it.next();
}
```

### 34.4 增强for循环，foreach

所有单列集合都可以使用，Collection继承了Iterable

原理就是使用了Iterator，所以遍历的时候不能进行增删操作

foreach只能用于集合或者数组

```
for(类型 变量名：集合/数组名){
    //...
}
```

## 35 List接口：集合

```java.util.List```是Collection的子类

1. 有序
2. 有索引
3. 允许重复

### 35.1 常用带索引的方法

```
public void add(int index, E element);将指定的元素，添加到该集合中的指定位置上

public E get(int index);返回集合中指定位置的元素

public E remove(int index);移除列表中指定位置的元素，返回被移除的元素

public E set(int index, E element);用指定元素替换集合中指定位置的元素，返回更新前的元素
```

### 35.2 ArrayList

List接口的大小可变的**数组**实现，此实现不是同步的

+ ArrayList增删都会复制一次数组

### 35.3 LinkedList

List接口的**链表**实现，此实现不是同步的
常用方法有对头尾操作的方法

```
public void addFirst(E e);
public void push(E e);//first
public void addLast(E e);

public E getFirst();
public E getLast();

public E removeFirst();
public E pop();//first
public E removeLast();

public boolean isEmpty();
```

### 35.4 Vector

目前不多用了，可增长的对象数组，是同步的

## 36 Set接口：集合

```java.util.Set```继承了Collection接口

1. 不允许重复
2. 没有索引

### 36.1 HashSet

1. 无序集合
2. 底层是个HashMap

此方法也是不同步的

#### 36.1.1 哈希值

对象的逻辑地址值，Object的toString里的地址值就是下面这个方法【toString是16进制的】

Object类下有方法可以获取对象的哈希值：```int hashCode()```【这个是10进制的】

该源码：

```
public native int hashCode();
```
native表示该方法调用的是本地操作系统的方法

String类重写了该方法

#### 36.1.2 哈希表

JDK1.8前，数组+链表
JDK1.8后：数组+链表；数组+红黑树（提高查询速度）

哈希冲突后，用链表挂在一起，如果超过了8个，就会转成红黑树

#### 36.1.3 不重复元素存储问题

哈希冲突后，会用equals()判断，一样就不存，不一样就存

#### 36.1.4 HashSet存储自定义方法

自定义hashCode和equals方法后，就可以自定义“重复”

### 36.2 LinkedHashSet

HashSet的子类
双向链表，可以保证元素有序

## 37 可变参数

定义方法时，当方法的参数列表数据类型已经确定，但是参数的个数不确定，就可以使用可变参数。

```
修饰符 返回值类型 方法名(数据类型...变量名){
    //...
}
```

可变参数的底层就是一个数组，会根据传入参数的个数不同，创建不同长度的数组。可以传入0个参数。

方法中的变量名就是一个数组

### 37.1 注意事项

1. 参数列表中只能有一个可变参数
2. 可变参数必须在参数列表的末尾

相当于传入：
参数类型[] 参数名
但是这种写法需要传入一个数组，可变参数写法直接传参数即可

## 38 Collections：操作集合的工具类

```java.utils.Collections```

### 38.1 常用方法

```
public static <T> boolean addAll(Collection<T> c, T... elements);往集合中批量添加元素

public static void shuffle(List<?> list);打乱集合顺序

public static <T> void sort(List<?> list);将集合中的元素按照默认规则（升序）进行排序

public static <T> void sort(List<T> list, Comparator<? super T>);将集合中单元素按照指定规则排序
```

### 38.2 sort方法相关的一些点

参与排序的类，要实现```Comparable<T>```接口，重写```compareTo```方法

```compareTo```方法返回一个int，**this减去参数就是升序**【负数说明小，就是升序】

```Comparator```也是一个接口，可以直接传一个它的匿名内部类，要重写compare方法，还是**o1-o2是升序**

## 39 Map接口：集合

```java.util.Map<K,V>```

```Map<K,V>```：

1. key不能重复
2. 一个key只能有一个值
3. 双列集合，元素成对存在，key和value
4. key和value的数据类型可以不同

### 39.1 HashMap<K,V>

无序、不同步

【HashSet就是只用了HashMap的key】

### 39.2 LinkedHashMap<K,V>：有序

HashMap<K,V>的子类：

### 39.3 Map接口常用方法

```
public V put(K key, V value);添加指定的键值对，key不存在，返回null；V存在，返回被替换掉的value

public V remove(Object key);删除指定的键对应的键值对，返回被删除元素的值，失败返回null

public V get(Object key);失败返回null

boolean containsKey(Object key);

public Set<K> keySet();获取所有的键，存在指定Set中

public Set<Map.Entry<K,V>> entrySet();获取所有的键值对对象，存在Set集合中
```

### 39.4 遍历

#### 39.4.1方法1

```keySet()```获取键的集合后，遍历该集合，再```get(key)```

#### 39.4.2 方法2

Map有一个嵌套类（内部类）：接口```Map.Entry<K,V>```

键值对对象

```Map.Entry<K,V>```中有方法：```getKey()```和```getValue()```

```entrySet()```获取entry集合，遍历entry集合，再用Entry的方法获取键值

### 39.5 HashMap存储自定义类

重写hashCode和equals方法来实现自定义的key唯一

### 39.6 Hashtable<K,V>

+ Map的另一个实现类，不允许存储null

+ 同步的

+ 不常用，被HashMap取代【如Vector被ArrayList取代】

+ 但Hashtable的子类Properties依然常用
Properties是唯一一个和IO流相结合的集合

## 40 集合添加方法的优化【jdk9】

List、Set、Map都添加了of()方法，在集合元素个数确定时使用

往集合中直接添加元素

```
static <E> List<E> of (E... elements)
```

### 40.1 注意

1. of方法只适用于List接口、Map接口、Set接口，不适用于接口的实现类
2. of的返回值是一个不能改变的集合，该集合不能再用add、put等方法添加元素，会抛异常
3. Set接口和Map接口在调用of方法的时候不能有重复的元素，否则会抛异常

调用：
```
List.of(1,2,3);
Set.of(1,2,3);
Map.of(k1,v1,k2,v2);
```
## 41 Debug

F8：逐行

F7：进入到方法中

shift+F8：跳出方法

F9：跳到下一个断点

Ctrl+F2：退出debug模式，停止程序

## 42 异常

java处理异常的方式是中断处理（并不是语法错误，语法错误编译就不通过）

### 42.1 异常体系

根类：```java.lang.Throwable```

有2个子类：```java.lang.Error```和```java.lang.Exception```

#### 42.1.1 Error

如内存溢出

#### 4.2.2 Exception

产生异常后，会产生一个Exception对象（包括内容、原因、位置）。如果一直没有人处理，抛出到JVM后，JVM就会中断处理并打印信息

Exception还有个子类：**RuntimeException**

### 42.2 异常的处理

try、catch、finally、throw、throws

#### 42.2.1 throw

在方法中抛出指定异常
```
throw new xxxException("异常原因");
```

注意：

1. throw必须写在方法内部
2. new的对象必须是Exception或者Exception的子类对象
3. throw创建的指定的异常，必须处理：
​	1. throw创建的是RuntimeException及其子类，可以不处理，交给JVM
​	2. throw创建的是编译异常，要么throws，要么catch

索引越界和空指针异常都是RuntimeException

### 42.2.2 throws

1. 必须写在方法声明的后面
2. 声明的异常必须是Exception及其子类
3. 如果方法内部抛出了多个异常，也要声明多个异常，用逗号隔开；如果有子父类关系，那么直接声明父类即可
4. 调用有throws的方法，就必须处理

### 42.2.3 try...catch

try中可能抛出多个异常，可以使用多个catch来处理这些异常
【catch会从上到下匹配，但是进了一个就不会进其他了】
【子类必须写在上面】

### 42.2.4 finally

最后一定会执行的代码块。

### 42.3 throwable中的三个方法

```
String getMessage();返回此throwable的简短描述【就是之前new的时候传进去的那个字符串】

String toString();返回此throwable的详细信息字符串【会加上异常名称加上上面的那个字符串】

void printStackTrace();打印栈轨迹【堆栈轨迹】
```

### 42.4 多个异常处理

1. 分别处理，每个写个try...catch...
2. 一次捕获多次处理，一个try，多个catch
3. 一次捕获，一次处理，catch里写公共父类

### 42.5 注意事项

1. finally里别写return，那样方法结果就不变了
2. 父类方法抛出多个异常，子类重写父类方法的时候。要么抛出相同的异常，要么抛出异常的子类，要么不抛出
3. 父类方法没有抛出异常，子类也不能抛出。如果子类有异常，只能catch【父类异常什么样，子类异常也什么样】

### 42.6 自定义异常

1. 需要一个空参数构造方法
2. 需要一个带异常信息（String）的构造方法
3. 名字以Exception结尾
4. 继承Exception或RuntimeException：如果继承Exception，就是编译器异常，必须处理；如果是继承RuntimeException，可以不处理，交给JVM

两个构造方法里都是调用父类的构造方法：
```super();```和```super(str)```

## 43 线程

### 43.1 线程与进程

线程调度：
+ 分时调度【轮流】
+ 抢占式调度【按优先级，同一个优先级随机选一个执行（效果还是轮流切）】（java）

其实多线程只是提高了CPU的使用率

### 43.2 创建线程类

主线程：执行main方法的进程

```java.lang.Thread```

创建执行线程有两种方法：

#### 43.2.1 方法一

**类声明为Thread的子类，重写run方法。**

创建一个子类对象，调用start方法就会启动。

```
void start();结果是两个线程并发地运行，当前线程（main线程）和另一个线程会并发的执行。只能启动一次。
```

start会开辟一个新的栈空间执行run方法

#### 43.2.2 方法二

**接口Runnable的实现类，实现run方法**

启动时需要创建一个Thread类，传入Runnable接口实现类的对象，再调用start方法

```
PrimeRun p = new PrimeRun();
new Thread(p).start()
```

### 43.3 Thread类构造方法

```
public Thread();

public Thread(String name);线程可以重名

public Thread(Runnable target);

public Thread(Runnable target, String name);

```

### 43.4 Thread类常用方法

```
public String getName();返回线程的名称

public static Thread currentThread();返回当前正在执行的线程对象的引用

public void setName(String name);改变线程名称

public static void sleep(long millis);当前执行的线程以毫秒数暂停
```

### 43.5 两种实现方法的区别

Runnable接口的好处：
1. 避免了单继承的局限性
2. 增强了程序的扩展性，降低了耦合性【把设置线程任务和开启线程分离】

### 43.6 匿名内部类实现线程创建

可以简化代码

#### 43.6.1 继承Thread类

```
new Thread(){
    重写run方法
}.start();
```

#### 43.6.2 实现Runnable接口

```
new Thread(
  new Runnable(){
      重写run方法
  }
).start();
```

## 44 线程安全

多线程访问共享数据

把一个Runnable的实现类的一个对象，重复传入到多个Thread中，访问的是共享数据。

### 44.1 线程同步

1. 同步代码块
2. 同步方法
3. Lock锁

### 44.2 同步代码块

```
synchronized(同步锁){
    需要同步操作的代码
}
```

注意：
1. 同步代码块中的同步锁对象，可以是任意对象
2. 多个线程使用的锁对象是同一个
3. 锁对象作用：只让一个线程在同步代码块中执行

### 44.3 同步方法

使用synchronized修饰的方法

```
public synchronized void method(){
    可能会产生线程安全问题的代码
}
```

+ 对于**非static**方法，同步锁就是this
+ 对于**static**方法，同步锁是当前方法所在类的字节码对象（类名.class）

### 44.4 Lock锁

```java.util.concurrent.locks.Lock```接口

方法：
```
void lock();获取锁
void unlock();释放锁
```

实现类：```java.util.concurrent.locks.ReentrantLock implements Lock```

使用：

**在成员变量的位置创建ReentrantLock对象，然后在可能出问题的代码前lock，后unlock。一般要把unlock写在finally里**

## 45 线程的状态

在```java.lang.Thread```里面有个嵌套类（内部类）```java.lang.Thread.State```描述了线程的状态

### 45.1 线程的6个状态

+ **NEW：新建状态**
```start()```后，有空闲CPU资源，则进入**运行状态**，没有进入**阻塞状态**

+ **RUNNABLE：运行状态**

+ **BLOCKED：阻塞状态**
运行状态和阻塞状态会互相切换

run方法结束，或调用了stop方法，就会进入死亡状态

+ **TERMINATED：死亡状态**

+ **TIMED_WAITING：休眠（睡眠）状态，计时等待**
在运行状态时，调用了sleep方法或带参数的wait方法```Object.wait(long)```进入睡眠状态

休眠结束会视CPU是否有空闲分别进入运行状态或阻塞状态


+ **WAITING：无限（永久）等待状态，植物人状态**
调用wait方法时不传参数，就会进入无限等待状态

调用Object.notify()就会唤醒，视CPU状态进入运行状态或阻塞状态

**只有锁对象才能调用wait()和notify()方法**

### 45.2 等待与唤醒

+ 进入到计时等待有2种方式
```
sleep(long m);
wait(long m);如果m毫秒后该线程没有被唤醒，就会自己醒来
```

+ 唤醒的方法：
```
notify();唤醒等待的单个线程
notifyAll();唤醒该监视器上的所有线程
```

+ 只有锁对象才能调用```wait()```和```notify()```方法，这两个方法必须要在同步代码块或同步函数中使用。

## 46 线程池

容器，一个集合【```ArrayList, LinkedList<Thread>```】

第一次启动的时候创建多个线程保存到一个集合里
使用的时候，remove或removeFirst取出一个，用完再add或addLast回去

JDK1.5之后，内置了线程池
里面的线程可以重复使用，省去了频繁创建销毁线程的操作

### 46.1 线程池代码实现

+ 生产线程池的工厂类：```java.util.concurrent.Executors```

```
static ExecutorService newFixedThreadPool(int nThreads)；创建一个可重用 固定线程数的线程池
```

+ 线程池接口：```java.util.concurrent.ExecutorService```

```
Future<?> submit(Runnable task);从线程池中获取线程，调用start方法，执行线程任务

void shutdown();销毁线程池（不建议执行）
```

## 47 Lambda表达式

JDK8加入

### 47.1 格式

一些参数、一个箭头、一段代码
```
(参数列表) -> {一段代码};
```
箭头是传递的意思。

### 47.2 书写

可推导，可省略。

凡是根据上下文推导出来的内容，都可以省略书写。

可以省略的内容：
1. 参数列表的数据类型
2. 参数列表中的参数如果只有一个，类型和参数列表的括号都可以省略
3. 如果代码只有一行，无论是否有返回值，都可以省略```{},return,;```。要省略这三个就一起省略。

### 47.3 使用前提

Lambda的使用前提：
1. 必须具有接口，而且接口里**有且仅有一个抽象方法**
2. 必须具有**上下文推断**：方法的参数类型为Lambda对应的接口类型。

+ 有且仅有一个抽象方法的接口，称为“函数式接口”。

## 48 File类

```java.io.File```类是文件和目录路径名的抽象表示形式，主要用于文件和目录的创建、查找和删除等操作

### 48.1 静态的成员变量：4个

```
static String pathSeparator;与系统有关的路径分隔符：Windows是分号，用来分隔路径的。Linux是冒号
static char pathSeparatorChar;

static String separator;默认名称分隔符，文件名称分隔符。Windows是\，Linux是/
static char separatorChar;
```

**注意，路径不区分大小写**

### 48.2 构造方法

```
File(String pathname);

File(String parent, String child);合并两个路径的时候中间可以什么都不加

File(File parent, String child);

还有一个传URL的
```

### 48.3 常用方法

#### 48.3.1 获取的方法

```
public String getAbsolutePath();返回绝对路径
public String getPath();将此File转换为路径名字符串
public String getName();返回此File表示的文件或目录的名称
public long length();返回此File表示的文件的长度；大小以字节为单位【文件夹返回0，如果路径不存在，返回0】
```

#### 48.3.2 判断的方法

```
public boolean exists();路径是否存在
public boolean isDirectory();是目录？如果不存在，false
public boolean isFile();是文件？如果不存在，false
```

#### 48.3.3 创建和删除的方法

```
public boolean createNewFile();如不存在，创建一个新的空文件。文件存在返回false。如创建文件的路径不存在会抛出异常。
public boolean delete();删除文件或目录，如目录中有内容不会删除，路径不存在，均会返回false
public boolean mkdir();创建目录，如文件夹，创建不了返回false
public boolean mkdirs():创建目录，包括任何必须但不存在的父目录
```

### 48.4 目录遍历

```
public String[] list();返回该目录下的文件和文件夹
public File[] listFiles();返回该目录下的文件和文件夹
```

如果该路径不存在或不是一个目录，抛出空指针异常。

+ 可以获得隐藏文件和文件夹

## 49 递归

+ 递归次数不能太多，会造成栈内存溢出。

+ 构造方法，禁止递归。

## 50 文件过滤器

File类里有两个和```listFiles```重载的方法，参数传递的就是过滤器

```
File[] listFiles(FileFilter filter);
File[] listFiles(FilenameFilter filter);
```

### 50.1 过滤File对象
```java.io.FileFilter```接口：用于过滤File对象

抽象方法：
```
boolean accept(File pathname);//pathname就是使用listFiles方法遍历目录得到的每一个文件对象
```

### 50.2 过滤文件名

```java.io.FilenameFilter```接口：用于过滤文件名

抽象方法：
```
boolean accept(File dir, String name);//dir，构造方法中传递的被遍历的目录；name，使用listFiles方法遍历目录得到的每一个文件名称
```

## 51 IO

|        | 输入流      | 输出流       |
| ------ | ----------- | ------------ |
| 字节流 | InputStream | OutputStream |
| 字符流 | Reader      | Writer       |

+ 输出流被构造后就会创建一个对应的文件。
+ 输入流被构造时就会去和对应文件建立连接，如果没有会报错。

### 51.1 下述的IO流

+ 字节输出流：OutputStream
  + FileOutputStream
  + BufferedOutputStream【缓冲流】
  + ObjectOutputStream 【序列化流】
  + PrintStream【打印流】

+ 字节输入流：InputStream
  + FileInputStream	
  + BufferedInputStream【缓冲流】
  + ObjectInputStream【反序列化流】

+ 字符输出流：Writer
  + FileWriter
  + BufferedWriter【缓冲流】
  + OutputStreamWriter【转换流】

+ 字符输入流：Reader
  + FileReader
  + BufferedReader【缓冲流】
  + InputStreamReader 【转换流】

## 52 字节流

### 52.1 字节输出流OutputStream

```java.io.OutputStrean```**抽象类**，是表示字节输出流的所有类的父类

定义了一些子类共性的成员方法：

```
public void close();关闭输出流，并释放与流相关的系统资源

public void flush();刷新输出流，并强制任何缓冲的输出字节 被写出

public void write(byte[] b);
public void write(byte[] b, int off, int len);写字节数组的一部分，off是开始索引，len是长度

public abstract void write(int b);
```

### 52.2 文件字节输出流FileOutputStream

子类```java.io.FileOutputStream```文件字节输出流

#### 52.2.1 构造方法

```
FileOutputStream(String name);
FileOutputStream(String name, boolean append);

FileOutputStream(File file);
FileOutputStream(File file, boolean append);

name和file：写入数据的目的地。
append：追加写开关
```

写入数据的过程：程序找java虚拟机，然后找操作系统，调用操作系统的方法写入数据

#### 52.2.2 write方法

+ write写入的整数会被存储为对应的2进制保存。记事本打开的时候，如果是0-127，就会根据ASCII表转换，如果是其他值，就会根据系统默认码表（中文系统GBK）

+ 一次写入多个字节：
如果第一个字节是0-127的正数。那么查询ASCII
如果第一个字节是负数，那么第一个字节和第二个字节会组合成一个中文，查询系统默认码表（GBK）

+ UTF-8里3个字符一个中文

+ 写字符串的时候：String类有方法getBytes()

#### 52.2.3 换行

```
Windows：\r\n
Linux：\n
mac：\r
```

### 52.3 字节输入流InputStream

```java.io.InputStream```**抽象类**，是表示字节输入流的所有类的父类

共性方法：

```
int read();读取一个字节，读取到文件末尾返回-1（继续也是-1）

int read(byte[] b);

void close();
```

### 52.4 文件字节输入流FileInputStream

子类```java.io.FileInputStream```文件字节输入流

#### 52.4.1 构造方法

```
FileInputStream(String name);
FileInputStream(File file);
```

参数：读取文件的数据源

读取数据还是调用的OS的方法

+ 注意每次调用read后指针都会发生变化，写while循环的话，循环判断语句里必须用一个变量接收read的值，在循环内使用该变量

#### 52.4.2 一次读取多个字节

```
int read(byte[] b);
```

2个问题：

1. 参数的作用：数组长度是声明的时候就指定了的，一般定义为1024（1kb）或1024的整数倍。缓冲作用，存储读取到的字节。（如果后面不足的话，只会替换掉一部分）
2. 返回值是什么：读取的有效字节个数。（小于等于数组长度，可以为-1）

#### 52.4.3 读到的字节转String

```
String(byte[] bytes);
String(byte[] bytes, int offset, int length);//在这里一般offset=0，length=len（即上面的那个返回值）
```

#### 52.4.4 释放资源

+ 同时有读写流，先关写的

## 53 字符流

字节流读取中文文件时遇到问题：

一个中文字符
GBK：2个字节
UTF-8：3个字节

每次读取一个字节就会乱码。

### 53.1 字符输入流Reader

```java.io.Reader```抽象类，字符输入流

共性的成员方法：

```
int read();读取单个字符并返回

int read(char[] cbuf);一次读取多个字符，读入数组

void close();关闭流并释放系统资源
```

### 53.2 文件字符输入流FileReader 

```java.io.FileReader extends InputStreamReader extends Reader```文件字符输入流

作用：把硬盘文件中的数据以字符的方式读取到内存中

#### 53.2.1 构造方法

```
FileReader(String fileName);文件路径

FileReader(File file);
```

#### 53.2.2 读入的char转String

构造方法：
```
String(char[] value);
String(char[] value, int offset, int count);
```

### 53.3 字符输出流Writer

```java.io.Writer```抽象类

共性成员方法：

```
abstract void write(int c);
void write(char[] cbuf);
void write(char[] cbuf, int off, int len);

void write(String str);
void write(String str, int off, int len);

void flush();
void close();
```

### 53.4 文件字符输出流FileWriter

```java.io.FileWriter extends OutputStreamWriter extends Writer```文件字符输出流

#### 53.4.1 构造方法

```
FileWriter(File file);
FileWriter(String fileName, boolean append);

FileWriter(String filename);
FileWriter(File file, boolean append);
```

## 54 IO异常的处理

### JDK1.7前

JDK1.7前，写try...catch...的时候，要把流变量的声明提到外面，同时赋个空值，用来调用close，在finally里也要再try...catch一次，还要处理空指针异常

### JDK1.7之后

try后面可以增加一个括号，定义流对象，不用写finally：

```
try(定义流对象;定义流对象;...){
    可能会产生异常的代码;
}
catch(异常类 变量名){
    异常的处理;
}
```

### JDK9之后

try的前面可以定义流对象，try后面的括号中可以直接引入流对象的名称，并自动释放，不用写finally
```
F f1 = new F();//定义一个流，但是这里也会抛异常，还是得throws
F f2 = new F();//定义一个流
try(f1,f2){
    ...
}catch(){}
```

## 55 Properties属性集合
```
java.util.Properties extends Hashtable<k,v> implements Map<k,v>
```
+ Properties类表示了一个持久的属性集。可以保存在流中或从流中加载。
+ Properties集合是唯一一个和IO流相结合的集合
+   可以使用方法store，把集合中的临时数据，持久化写入到硬盘中存储。
+   可以使用方法load，可以把硬盘中保存的文件（键值对），读取到集合中使用

+ 属性列表中每个键及其对应值都是一个字符串

+ Properties集合是一个双列集合，key和value默认都是字符串

### 55.1 一些方法

```
Object setProperty(String key, String value);调用Hashtable的方法put

String getProperty(String key);通过key找到value，相当于Map中的get(key)

Set<String> stringPropertyNames();返回此属性列表中的键集合，相当于Map中的keySet方法
```

### 55.2 store方法

把集合中的临时数据，持久化写入到硬盘中存储

```
void store(OutputStream out, String comments);
void store(Writer writer, String comments);
```

+ 参数：
  OutputStream out：字节输出流，不能写入中文
  Writer writer：字符输出流，可以写中文
  String comments：注释，用来解释说明保存的文件的用途，不能用中文，会产生乱码，默认是Unicode编码。

### 55.3 load方法

把键值对文件读取到内存

```
void load(InputStream inStream);
void load(Reader reader);
```

注意：

存储键值对的文件中：
1. 键与值之间的连接符号可以用=，可以用空格
2. 可以用#注释，被注释的键值对不会被读取
3. 键值都默认是字符串，不用加引号

### 55.4 例子

新建一个配置文件，后缀名properties

```java
1. 加载配置文件
Properties pro = new Properties();
ClassLoader cl = ReflectTest.class.getClassLoader();//当前类的.class下的方法，getClassLoader()，获取类加载器
InputStream is = classLoader.getResourceAsStream("pro.properties");//资源对应的字节流
pro.load(is);
2. 获取配置文件中的内容
String a = pro.getProperty("keyName");
```

## 56 缓冲流

对基本流对象的一种增强，也叫高效流。增加一个缓冲区，减少IO。

### 56.1 BufferedOutputStream字节缓冲输出流
```java.io.BufferedOutputStream extends OutputStream```字节缓冲输出流

#### 56.1.1 继承自父类的方法：

```
close();
flush();
write();
```

#### 56.1.2 构造方法

```
BufferedOutputStream(OutputStream out);缓冲区大小默认
BufferedOutputStream(OutputStream out, int size);指定缓冲区的大小
```

### 56.2 BufferedInputStream字节缓冲输入流

```java.io.BufferedOutputStream extends OutputStream```字节缓冲输入流

#### 56.2.1 继承自父类的方法：

```
close();
read();
```

#### 56.2.2 构造方法

```
BufferedInputStream(InputStream in);缓冲区大小默认
BufferedInputStream(InputStream in, int size);指定缓冲区的大小
```

### 56.3 BufferedWriter字符缓冲输出流

```java.io.BufferedWriter extends Writer```字符缓冲输出流

#### 56.3.1 继承自父类的方法：

```
write();
close();
flush();
```

#### 56.3.2 构造方法

```
BufferedWriter(Writer out);缓冲区大小默认
BufferedWriter(Writer out, int sz);指定缓冲区的大小
```

#### 56.3.3 特有的成员方法

```
void newLine();写入一个行分隔符，会根据不同的操作系统获取不同的分隔符。println就是调用了这个
```

### 56.4 BufferedReader字符缓冲输入流

```java.io.BufferedReader extends Reader```字节缓冲输入流

#### 56.4.1 继承自父类的方法：

```
close();
read();
```

#### 56.4.2 构造方法

```
BufferedReader(Reader in);缓冲区大小默认
BufferedReader(Reader in, int sz);指定缓冲区的大小
```

#### 56.4.3 特有的成员方法

```
String readLine();读取一行文本。返回值为该行的内容字符串，不包含终止符。如果达到流末尾，返回null
```

注意：
```
.的转义是\\.【\需要一个\\来转义，然后再转义.，正则表达式里会用到】
```

## 57 转换流

### 57.1 字符编码

字符集：
ASCII字符集--ASCII编码表
GBK字符集--GBK编码
Unicode字符集--UTF8编码、UTF16编码、UTF32编码

转换流可以指定编码方式

### 57.2 OutputStreamWriter

```java.io.OutputStreamWriter extends Writer```

字符流通向字节流的桥梁，使用指定charset把写入流中的字符编码成字节。

#### 57.2.1 继承父类的方法

```
write();
flush();
close()
```

#### 57.2.2 构造方法

```
OutputStreamWriter(OutputStream out);默认编码，utf-8
OutputStreamWriter(OutputStream out, String charsetName);指定字符集，不区分大小写
```

### 57.3 InputStreamReader

```java.io.InputStreamReader extends Reader```
字符流通向字节流的桥梁，指定码表读取，解码。

#### 57.3.1 继承父类的方法

```
read();
close()
```

#### 57.3.2 构造方法

```
InputStreamReader(InputStream in);默认编码，utf-8
InputStreamReader(InputStream in, String charsetName);指定字符集，不区分大小写
```

+ FileReader 继承自 InputStreamReader ，InputStreamReader  继承自 FileInputStream

## 58 序列化与反序列化

### 58.1 序列化流ObjectOutputStream

```java.io.ObjectOutputStream extends OutputStream```

把对象以流的方式，写入到文件保存。对象的序列化。

#### 58.1.1 构造方法

```
ObjectOutputStream(OutputStream out);
```

#### 58.1.2 特有的成员方法

```
void writeOject(Object obj);
```

#### 58.1.3 Serializable接口

序列化和反序列的类必须实现Serializable接口。

+ 标记型接口。```java.io.Serializable```
  这个接口里什么都没有

### 58.2 反序列化ObjectInputStream

```java.io.ObjectInputStream extends InputStream```

#### 58.2.1 构造方法

```
ObjectInputStream(InputStream in);
```

#### 58.2.3 特有的成员方法

```
Object readObject();声明了ClassNotFoundException
```

### 58.3 transient关键字

瞬态关键字

static：静态关键字。静态优先于非静态加载到内存中（静态优先于对象进入到内存中）。所以static修饰的成员变量不能被序列化。

被transient修饰的关键字，不能被序列化。

### 58.4 反序列化还可能会遇到InvalidClassException

+ 序列化的过程中：
类实现了Serializable接口，就会给类的.class文件添加一个序列号serialVersioUID，会一起保存在序列化的字节内容中。
+ 反序列化的过程中：
会比较文件中的序列号与.class文件的序列号，一样则成功，不一样则抛出InvalidClassException

+ 如果类进行过修改，那么自然会不一样。

+ 可以手动给类添加序列号，让类无论如何修改，都不改变序列号。实现了Serializable接口的类可以声明一个static final修饰的成员变量serialVersionUID。
  ``` private static final long serialVersionUID = 1L;```

### 58.5 序列化集合

想保存多个对象的时候
可以把多个对象存储到一个集合中
对集合进行序列化和反序列化

## 59 打印流

```java.io.PrintStream```打印流

特点：
1. 只负责数据的输出，不负责数据的读取
2. 与其他输出流不同，PrintStream永远不会抛出IOException
3. 有特有的方法，print，println

### 59.1 构造方法

```
PrintStream(File file);输出目的地是一个文件
PrintStream(OutputStream out);输出目的地是一个字节输出流
PrintStream(String fileName);输出目的地是一个文件路径
```

```PrintStream extends OutputStream```

### 59.2 继承自父类的方法

```
close();
flush();
write();
```
### 59.3 注意

如果使用继承父类的write方法，会查询编码
如果使用print/println方法，写的数据原样输出

### 59.4 改变输出语句的目的地

打印流的流向
输出语句，默认在控制台输出
使用System.setOut方法改变输出语句的目的地。改为参数中传递的打印流的目的地
```
static void setOut(PrintStream out);
```
写完这句话后，sout语句的输出就会输出到文件

## 60 TCP通信程序

通信的两端，要严格区分客户端（Client）与服务端（Server）

服务器端有一个方法，accept方法，可以获取到请求的客户端对象

服务器使用客户端的流和客户端交互

### 60.1 客户端

表示客户端的类：

```java.net.Socket```此类实现客户端套接字（也可以就叫“套接字”）。

套接字是两台机器间通信的端点。套接字：包含了IP地址和端口号的网络单位。

#### 60.1.1 构造方法

```
Socket(String host, int port);//host，主机名称或IP地址
```

#### 60.1.2 成员方法
```
OutputStream getOutputStream();返回此套接字的输出流
InputStream getInputStream();返回此套接字的输入流
void close();关闭此套接字
```
#### 60.1.3 实现步骤

1. 创建客户端对象Socket，构造方法绑定服务器的IP地址和端口号
2. getOutputStream方法获取网络字节输出流OutputStream对象
3. 使用OutputStream对象的方法write，给服务器发送数据
4. getInputStream获取输入流对象
5. 使用输入流的read，读取数据
6. 释放资源

#### 60.1.4 注意
1. 交互必须用Socket中提供的网络流
2. 客户端Socket对象创建时，就会去和服务器三次握手建立通路，如果服务器没开，就会抛出异常。

### 60.2 服务器
```java.net.ServerSocket```

#### 60.2.1 构造方法
```
ServerSocket(int port);
```

#### 60.2.2 成员方法
```
Socket accept();获取请求的客户端对象Socket
```

+ 注意，使用完要把Socket和ServerSocket都关掉

### 60.3 注意
```read()```方法如果读取不到结束标记，就会进入阻塞状态

解决：
上传完文件后，给服务器写一个结束标记。
Socket类中的方法

```
void shutdownOutput();
```

### 60.4 BS服务器

读请求信息的第一行，就能获得要的文件地址。然后传回
传回前HTML协议响应头固定写法
HTTP/1.1 200 OK .....

如果一个网页有图片，客户端会开多个线程多次分别请求。服务器也就得写成一个死循环不断侦听

## 61 函数式编程

使用**Lambda**或**方法引用**简化程序

### 61.1 Lambda的延迟执行
举例：日志案例的性能优化
如果写成```function(level:1, message拼接)```这样，无论日志等级是几，都会拼接字符串
但如果写成```funtion(level, interface)```，然后调用的时候用Lambda表达式，那么只有当level为1时，才会调用Lambda表达式里的函数，不是不调用。

+ 提升性能

### 61.2 Lambda表达式作为函数的参数和返回值举例

参数：线程Runnable的run方法
返回值：Comparator的compare方法

## 62 函数式接口

有且仅有一个抽象方法的接口。
适用于函数式编程场景的接口。Java中的体现就是Lambda。

+ 语法糖：
使用更方便，但原理不变的代码语法。如foreach和迭代器。
Lambda从应用层面看上去是匿名内部类的语法糖，但二者原理不同。

### 62.1 注解@FuntionalInterface

作用：可以检测接口是否是一个函数式接口

### 62.2 使用

作为函数参数，使用Lambda表达式

### 62.3 Lambda与匿名内部类的区别

没有class文件，不用加载，提高效率

## 63 常用的函数式接口

主要在```java.util.function```包里

### 63.1 Supplier

```java.util.function.Supplier<T>```仅包含一个无参的方法：```T get()```。用来获取一个泛型参数指定类型的对象

```Supplier<T>```接口被称之为生产型接口，指定接口的泛型是什么类型，那么接口中的get方法就会生产什么类型的数据

### 63.2 Consumer

```java.util.function.Consumer<T>```消费数据
包含抽象方法```void accept(T t);```

#### 63.2.1 默认方法andThen

作用：需要两个Consumer接口，可以把两个Consumer接口组合到一起，对数据进行消费
```
Consumer<String> con1;
Consumer<String> con2;
String s = "hello";

con1.andThen(con2).accept(s);谁写前面谁先消费
这里可以继续andThen，con1.andThen(con2).andThen(con3)...
相当于
con1.accept();
con2.accept();
```

### 63.3 Predicate接口
```java.util.function.Predicate<T>```作用：对某种数据类型的数据进行判断，结果返回一个boolean值。抽象方法```boolean test(T t);```来判断。

#### 63.3.1 默认方法
+ and：与
```
pre1.and(pre2).test(t);
等价于
pre1.test(t) && pre2.test(t)
```

+ or：或

+ negate：非

### 63.4 Function接口
```java.util.function.Function<T,R>```接口用来把前一个类型的数据转换成另一个类型的数据，前者称为前置条件，后者称为后置条件。方法```R apply(T t);```

#### 63.4.1 默认方法andThen
和Consumer的差不多

## 64 Stream流

JDK1.8之后出现。关注于做什么

### 64.1 获取一个流

方法一：所有**Collection集合**都可以通过stream默认方法获取流
```
default Stream<E> stream();
```

方法二：Stream接口的静态方法of可以获取**数组**对应的流
```
static <T> Stream<T> of (T... values);参数是一个可变参数，可以传入一个数组
```

### 64.2 方法分类

分为两类：延迟方法和终结方法。

+ 延迟方法的返回值还是流，可以链式调用。
+ 终结方法不行。有2个，count和forEach

### 64.3 Stream流的特点

Stream流属于管道流，只能被消费（使用）一次
第一个Stream流调用完毕，数据就会流到下一个Stream上，而这时第一个Stream流就会关闭，不能再调用。

### 64.4 常用方法

+ forEach
逐一处理
终结方法
```
void forEach(Consumer<? super T> action);
```

+ count
统计个数
终结方法
```
long count();
```

+ filter
过滤，返回一个新的流
```
Stream<T> filter(Predicate<? super T> predicate);
```

+ map
映射
```
<R> Stream<R> map(Function<? super T, ? extends R> mapper);
```

+ limit
取用前几个
```
Stream<T> limit(long maxSize);集合长度大于参数才截取，否则不进行操作
```

+ skip
跳过前几个
```
Stream<T> skip(long n);如果流的长度小于n，会得到一个长度为0的空流
```

+ concat
组合
两个流合并成一个流
```
static <T> Stream<T> concat(Stream<? extend T> a, Stream<? extend T> b);
```

## 65 方法引用

```::```引用运算符，它所在的表达式被称为方法引用

用来简化Lambda表达式，对象和方法都已经存在，参数可以省略

+ 通过对象名引用成员方法
前提是对象已经存在，成员方法也已经存在

+ 通过类名引用静态方法

+ 通过super引用父类的成员方法

+ 通过this引用本类的成员方法

+ 类的构造器引用
```类名称::new```

+ 数组的构造器引用
```int[]::new```

## 66 Junit单元测试

测试分类：
  1. 黑盒测试
  2. 白盒测试：Junit是白盒测试

IDEA使用技巧：/** 回车 可以快速生成默认注释

### 66.1 使用步骤：

1. 定义一个测试类（测试用例）
测试类名：被测试的类名Test
包名：xxx.xxxx.xx.test

2. 定义测试方法：可以独立运行
方法名：test测试的方法名
返回值：void
参数列表：空参
	
3. 给方法加注解```@Test```

4. 导入依赖环境alt+enter

就可以直接运行该方法了

### 66.2 判定结果

不看输出，看红色（失败）还是绿色（正确）。后期有测试框架

### 66.3 断言Assert

```
Assert.assertEquals(String message, Object expected, Object actual);
```

### 66.4 两个注解：Before和After

+ ```@Before```
用于资源申请之类的，所有测试方法在执行之前都会先执行该方法

+ ```@After```
所有测试方法最后都会执行该方法。即使有异常也会执行。

## 67 反射

反射是框架设计的灵魂

框架：半成品的软件。

反射：将类的各个组成部分封装为其他对象，这就是反射机制。

字节码文件会被类加载器加载到内存中，封装成Class类的对象
成员变量封装成Field对象
构造方法ConStructor
成员方法Method。
由Class类对象再去new自定义类的对象

### 67.1 反射的好处

1. 可以在程序运行的过程中，操作这些对象。
2. 可以解耦，提高程序的可扩展性。

### 67.2 获取Class对象的方式：

```
Class.forName("全类名");
```
将字节码文件加载进内存，返回Class对象。多用于配置文件，将类名定义在配置文件中。读取文件，加载类。

```
类名.class
```
通过类名的属性class获取。	多用于参数的传递
```
对象.getClass()
```
Object类中的方法。用对象获取字节码


+ **注意**：
同一个字节码文件在一次程序运行过程中，只会被加载一次，不论通过哪一种方式获取的Class对象都是同一个。


### 67.3 获取功能

#### 67.3.1 获取成员变量们

```
Field[] getFields();获取public的成员变量

Field[] getField(String name);指定public成员变量的名称

Field[] getDeclaredFields();获取所有的成员变量，不考虑修饰符

Field[] getDeclaredField(String name);
```

#### 67.3.2 获取构造方法们

```
Constructor<?>[] getConstructors();

Constructor<?>[] getConstructor(Class<?>... parameterTypes);区分构造方法是靠传入的参数，这里的参数就是传入参数的class对象，如：String.class,int.class

Constructor<?>[] getDeclaredConstructors();

Constructor<?>[] getDeclaredConstructor(Class<?>... parameterTypes);
```

#### 67.3.3 获取成员方法们

```
Method[] getMethods();

Method[] getMethod(String name, Class<?>... parameterTypes);

Method[] getDeclaredMethods();

Method[] getDeclaredMethod(String name, Class<?>... parameterTypes);
```

#### 67.3.4 获取类名

```
String getName();
```

IDEA使用技巧：iter出现的就是for-each

### 67.4 操作

#### 67.4.1 Field：成员变量


1. 设置值
```
void set(Object obj, Object value);
```
2. 获取值
```
Object get(Object obj);要传个Object类的对象
```

访问非public的成员变量时，要忽略访问权限修饰符的安全检查：
```
d.setAccessible(true);//d就是private的变量名。暴力反射
```

#### 67.4.2 Constructor:构造方法

```
T newInstance(Object... initargs);//创建对象

T personClass.newInstance();//1.9后过时。Class里的方法，使用空参数的构造方法创建对象
```

#### 67.4.3 Method:方法对象

```
Object invoke(Object obj, Object... args);//传一个Object对象和参数列表，执行方法

String getName();获取方法名
```

## 68 注解

作用：编写文档，编译检查，代码分析

### 68.1 常用的3个注解

```
@Override
@Deprecated该注解标注的内容，表示已过时
@SuppressWarnings压制警告，需要传参，一般“all”
```

### 68.2 自定义注解

#### 68.2.1 格式：

```
元注解
public @interface 注解名称{
属性列表;
}
```

+ 反编译：命令行窗口javap

+ 注解本质上就是一个接口，该接口默认继承java.lang.annotation.Annotation接口

#### 68.2.2 属性：接口中的抽象方法

要求：
1. 属性的返回值类型：基本数据类型，String，枚举，注解，以上类型的数组
2. 定义了属性，在使用时需要给属性赋值

```
@MyAnno(age = 1,name="a")
String name() default "b";
```

+ 如果只有一个属性需要赋值，并且属性的名称是value，则value可以省略

返回值举例：
```
per = Person.P1//枚举
anno2 = @MyAnno2//注解
strs = {"",""}只有1个时大括号可以省略//数组
```

#### 68.2.3 元注解

用于描述注解的注解

```
@Target：描述注解能够作用的位置。
ElementType枚举类：TYPE作用于类，METHOD作用于方法，FIELD作用于成员变量上

@Retention：描述注解能被保留的阶段。
RetentionPolicy枚举类：CLASS RUNTIME SOURSE，一般都用RUNTIME

@Documented：注解是否被抽取到api文档中javadoc

@Inherited：描述注解是否被子类继承
```

### 68.3 在程序中使用（解析）注解

1. 获取注解定义的位置的对象：Class/Method/Field。这里以定义在类上为例，获取类的字节码文件对象
```
Class<ReflectTest> rc = ReflectTest.class
```

2. 获取注解
```
Pro an = rc.getAnnotation(Pro.class);
这里的Pro是自定义的一个注解。其实就是在内存中生成了一个该注解接口的子类实现对象
```

3. 调用注解对象的方法获取当前类（ReflectTest）上的注解（Pro）配置的属性值
```
String className = an.className();
```

+ 判断方法上是否有注解 method.isAnnotationPresent(Pro.class)

### 68.4 异常处理

由于反射机制，我们直接catch到的异常是：```java.lang.reflect.InvocationTargetException```，需要调用getCause拿到真正的异常。

```
e.getCause().getClass().getSimpleName();
e.getCause().getMessage();
```

### 68.5 小结

1. 大多数时候，使用注解，而不是自定义注解

2. 注解给编译器用，给解析程序用

3. 注解不是程序的一部分，可以理解为一个标签