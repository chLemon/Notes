### 5.2 选择语句switch

+ 记得写    default：和        break;


## 10 Scanner类

```
Scanner sc = new Scanner(System.in);
String str = sc.next();
int num = sc.nextInt();
```

## 12 ArrayList类

+ 注意事项：
对于ArrayList集合来说，直接打印得到的不是地址值，而是内容。如果内容是空，得到的是空的中括号：[]

### 12.2 常用方法和遍历

```
public boolean add(E e);
public E get(int index);
public E remove(int index);
public int size();
```

### 13.4 String常用方法
#### 13.4.1 内容比较

```
public boolean equals(Object obj);//推荐把常量写在前面，如："abc".equals(str),变量可能会是null，.的时候会报错

public boolean equalsIgnoreCase(String str);//忽略大小写，进行内容比较
```
控制台输出exception信息可能会断开，红字中间夹杂着黑字

#### 13.4.3 截取方法

```
public String substring(int index); 截取从参数位置一直到字符串末尾，返回新字符串

public String substring(int begin, int end); 截取一段字符串，左闭右开
使用：
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

## 16 数学工具类Math

```java.util.Math```类是数学相关的工具类

```
public static double abs(double num);获取绝对值，有多重重载int long float double

public static double ceil(double num);向上取值

public static double floor(double num);向下取整

public static long round(double num);四舍五入

Math.PI近似的圆周率
```

### 19.2 注意

1. 接口不能有**静态代码块**或者**构造方法**。

## 22 内部类

分类：
1. 成员内部类
2. 局部内部内（包含匿名内部类）

### 22.1 成员内部类

成员内部类的定义格式：

+ 内用外，随意访问（包括private）；外用内，需要**内部类对象**。

+ 内部类的字节码文件：Body$Heart.class

#### 22.1.1 使用成员内部类

直接方式：

```
外部类名称.内部类名称 对象名 = new 外部类名称().new 内部类名称();
```

#### 22.2.1 注意

类的权限修饰符：
1. 外部类：public、（default）
2. 成员内部类：public、protected、（default）、private
3. 局部内部类：什么都不能写

+ 局部内部类如果想访问所在方法的局部变量，那么这个局部变量必须是【有效final】的。
即，要么是final的，要么可以省略final，但是确实事实不变。

+ 原因：生命周期不一样。局部变量跟方法，在栈内存里，方法结束出栈局部变量就消失了。而内部类new出来的对象在堆中持续存在，直到回收。所以得让变量不变，才方便留一个副本在对象中。

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

## 28 Calendar类

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

### 30.2 常用方法

```
public StringBuilder append(...);添加任意类型数据的字符串形式，并返回【当前对象自身】，该方法无需接收返回值
```

#### 31.1.2 拆箱

##### 31.1.2.1 成员方法

```
int intValue();以int类型返回该Integer的值
```

## 32 基本类型与字符串类型的相互转换

### 32.2 字符串转基本类型

包装类的静态方法parseXXX(String str)

### 33.2 定义含有泛型的方法

```
修饰符 <泛型> 返回值类型 方法名(M m){//在参数列表处可以使用泛型
    //方法体
}
```

使用的时候直接传参，参数是什么类型，泛型就是什么类型

## 34 Collection接口：集合

### 34.1 集合框架

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

public boolean remove(E e);从集合中删除给定对象

public boolean isEmpty();判断当前集合是否为空

public Object[] toArray();把集合中的元素存储到数组中	
```

## 35 List接口：集合

```java.util.List```是Collection的子类

### 35.1 常用带索引的方法

```
public void add(int index, E element);将指定的元素，添加到该集合中的指定位置上

public E get(int index);返回集合中指定位置的元素

public E remove(int index);移除列表中指定位置的元素，返回被移除的元素

public E set(int index, E element);用指定元素替换集合中指定位置的元素，返回更新前的元素
```

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

## 38 Collections：操作集合的工具类

```
public static <T> boolean addAll(Collection<T> c, T... elements);往集合中批量添加元素

public static void shuffle(List<?> list);打乱集合顺序

public static <T> void sort(List<?> list);将集合中的元素按照默认规则（升序）进行排序

public static <T> void sort(List<T> list, Comparator<? super T>);将集合中单元素按照指定规则排序
```

## 39 Map接口：集合

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

boolean containKey(Object key);

public Set<K> keySet();获取所有的键，存在指定Set中

public Set<Map.Entry<K,V>> entrySet();获取所有的键值对对象，存在Set集合中
```

### 39.6 Hashtable<K,V>

+ Map的另一个实现类，不允许存储null

+ 同步的

+ 不常用，被HashMap取代【如Vector被ArrayList取代】

+ 但Hashtable的子类Properties依然常用
Properties是唯一一个和IO流相结合的集合

### 42.5 注意事项

2. 父类方法抛出多个异常，子类重写父类方法的时候。要么抛出相同的异常，要么抛出异常的子类，要么不抛出
3. 父类方法没有抛出异常，子类也不能抛出。如果子类有异常，只能catch【父类异常什么样，子类异常也什么样】

## 43 线程

### 43.4 Thread类常用方法

```
public String getName();返回线程的名称

public static Thread currentThread();返回当前正在执行的线程对象的引用

public void setName(String name);改变线程名称

public static void sleep(long millis);当前执行的线程以毫秒数暂停
```

## 44 线程安全

多线程访问共享数据

把一个Runnable的实现类的一个对象，重复传入到多个Thread中，访问的是共享数据。

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

#### 56.1.2 构造方法

```
BufferedOutputStream(OutputStream out);缓冲区大小默认
BufferedOutputStream(OutputStream out, int size);指定缓冲区的大小
```

#### 56.2.2 构造方法

```
BufferedInputStream(InputStream in);缓冲区大小默认
BufferedInputStream(InputStream in, int size);指定缓冲区的大小
```

### 56.3 BufferedWriter字符缓冲输出流

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
类实现了Serializable接口，就会给类的.class文件添加一个序列号serialVersionUID，会一起保存在序列化的字节内容中。
+ 反序列化的过程中：
会比较文件中的序列号与.class文件的序列号，一样则成功，不一样则抛出InvalidClassException

+ 如果类进行过修改，那么自然会不一样。

+ 可以手动给类添加序列号，让类无论如何修改，都不改变序列号。实现了Serializable接口的类可以声明一个static final修饰的成员变量serialVersionUID。
  ``` private static final long serialVersionUID = 1L;```

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

## 61 函数式编程

使用**Lambda**或**方法引用**简化程序

### 62.1 Lambda的延迟执行
举例：日志案例的性能优化
如果写成```function(level:1, message拼接)```这样，无论日志等级是几，都会拼接字符串
但如果写成```funtion(level, interface)```，然后调用的时候用Lambda表达式，那么只有当level为1时，才会调用Lambda表达式里的函数，不是不调用。

+ 提升性能

## 62 函数式接口

有且仅有一个抽象方法的接口。
适用于函数式编程场景的接口。Java中的体现就是Lambda。

### 61.1 注解@FuntionalInterface

作用：可以检测接口是否是一个函数式接口

### 61.2 使用

作为函数参数，使用Lambda表达式

### 61.3 Lambda与匿名内部类的区别

没有class文件，不用加载，提高效率

## 66 Junit单元测试

### 66.3 断言Assert

```
Assert.assertEquals(String message, Object expected, Object actual);
```

## 67 反射

成员变量封装成Field对象
构造方法ConStructor
成员方法Method。
由Class类对象再去new自定义类的对象


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
```

#### 67.4.3 Method:方法对象

```
Object invoke(Object obj, Object... args);//传一个Object对象和参数列表，执行方法

String getName();获取方法名
```

