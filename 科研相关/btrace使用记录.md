> 本文参考了《如何在生产环境使用BTrace进行调试》https://www.jianshu.com/p/dbb3a8b5c92f，与BTrace的GitHub文档。

BTrace是一个Java 动态、安全追踪（监控）工具，可以在不用重启的情况下监控系统运行情况，方便的获取程序运行时的数据信息，如方法参数、返回值、全局变量和堆栈信息等。

最近用到了该工具，稍微记录一下自己使用时遇到的一些点，详细使用请看GitHub内的文档。

项目地址：https://github.com/btraceio/btrace

docs内有提供详细的使用说明。

**注意：BTrace能做的事情太多，但使用之前切记检查脚本的可行性，一旦BTrace脚本侵入到系统中，只有通过重启才能恢复。**

**BTrace会对原程序的性能有非常大的影响，谨慎使用。**

## 导包问题

BTrace脚本内只能使用BTrace.Utils里面定义的一些方法。BTrace在2.0更新后，包名发生了变化，导包的时候务必打开提供的samples里看一下前缀是什么。我使用的是1.3的版本。

## 访问被拒绝

我在使用的时候出现了访问被拒绝的情况。BTrace命令带上参数```-v```可以输出更详细的日志。可以用来排查问题。

我遇到访问被拒绝的问题，是由于，BTrace想要让运行中的程序监听2020端口，而这个端口已经被占用了。排查了一下发现是我的Chrome浏览器占用了端口，关掉浏览器就好了。

## 一个例子

```java
import com.sun.BTrace.annotations.*;
import static com.sun.BTrace.BTraceUtils.*;
import com.sun.BTrace.services.impl.Printer;

@BTrace
public class AllMethods {
    @Injected(ServiceType.RUNTIME)
    private static Printer printer;

    @OnMethod(
        clazz="/HelloWorld/",
        method="/.*/"
    )
    public static void m(@Self Object o, @ProbeClassName String probeClass, @ProbeMethodName String probeMethod) {
        printer.print("entered " + probeClass);
        printer.println("." + probeMethod+"   TIME:"+ Time.millis());
    }
}
```

# 两个主要注解

## @OnMethod

BTrace使用```@OnMethod```注解指定需要拦截的方法

在该注解内，需要指定clazz和method属性，来定位要拦截的方法。clazz指定要拦截的类，method指定要拦截的方法。

clazz和method既可以使用全名，也可以使用正则表达式。在clazz中使用```+```可以表示接口/类的全部实现类/子类。

该注解内还可以指定location属性，其作用在```@Location```注解部分中记录。

## @Location
该注解主要用来指定对方法拦截的位置，如在方法进入的时候进行拦截，还是在方法返回前进行拦截。属性value默认取值为Kind.ENTRY，在方法进入的时候拦截。

除value外，该注解内还有属性clazz，method，where。主要用于拦截当前方法内调用的其他方法。

# 几个案例

## 1 获取当前拦截的方法的名称

```java
@BTrace
public class HelloWorldTrace {
    @OnMethod(clazz="extra.HelloWorld")
    public static void onMethod(@ProbeMethodName String pmn) {
        println("Hello from method " + pmn);
    }
}
```

## 2 获取当前拦截的方法的声明语句（修饰符 返回值 名称 参数类型）

``` java
@BTrace
public class HelloWorldTrace {
    @OnMethod(clazz="extra.HelloWorld", method="/call.*/")
    public static void onMethod(@ProbeMethodName(fqn = true) String pmn) {
        println("Hello from method " + pmn);
    }
}
```

## 3 获取一个类或接口的  所有子类和实现类的 方法

``` java
@BTrace
public class HelloWorldTrace {
    @OnMethod(clazz="+extra.HelloWorld", method="/call.*/")
    public static void onMethod(@ProbeMethodName(fqn = true) String pmn) {
        println("Hello from method " + pmn);
    }
}
```

## 4 获得方法的执行时间

需要使用注解```@Location(Kind.RETURN)```，dur返回的时间单位是纳秒

``` java
@BTrace
public class HelloWorldTrace {
    @OnMethod(clazz="extra.HelloWorld", method="/call.*/", location=@Location(Kind.RETURN))
    public static void onMethod(@ProbeMethodName(fqn = true) String pmn, @Duration long dur) {
        println("Hello from method " + pmn);
        println("It took " + str(dur) + "ns to execute this method");
    }
}
```

# @OnTimer

该注解可以设置周期执行BTrace脚本

该注解的参数的单位是**毫秒**

该注解修饰的方法的返回值必须是```void```

``` java
@BTrace
public class HelloWorldTrace {
    @OnTimer(1000)
    public static void ontimer() {
        println("tick ...");
    }
}
```

# 采样拦截

一直拦截许多方法可能会造成性能急剧下降。通常我们对数据的颗粒度要求并不是非常高（采样间隔不用特别小）。因此可以使用统计采样来减少收集的数据量和相关开销。

无论如何设置，BTrace的采样都会保证至少进行一次拦截。

## 拦截1/10的调用

``` java
@BTrace
public class HelloWorldTrace {
    private static int cntr = 1;
    @Sampled(kind = Sampled.Sampler.Const, mean = 10)
    @OnMethod(clazz="/extra\\.HelloWorld.*/", method="callD")
    public static void onMethod(@ProbeMethodName(fqn = true) String pmn) {
        println("Hello from method " + pmn + " : " + (cntr++));
    }
}
```

## 动态调整mean参数

这种模式下，mean的取值实际上指定的是，两次拦截间的间隔时间的最低的纳秒数。

mean的最小值为180.

### 获取调用次数

``` java
@BTrace
public class HelloWorldTrace {
    private static int cntr = 1;
    @Sampled(kind = Sampled.Sampler.Adaptive, mean = 50)
    @OnMethod(clazz="/extra\\.HelloWorld.*/", method="callD")
    public static void onMethod(@ProbeMethodName(fqn = true) String pmn) {
        println("Hello from method " + pmn + " : " + (cntr++));
    }
}
```
