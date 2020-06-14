[TOC]
# Java基础
## 语言特点
* 面向对象和面向过程对比。
    * 面向过程 性能好。
    * 面向对象 容易写出低耦合的代码。利于维护和扩展、复用
* 面向对象的4大特性 封装 继承 多态 抽象
    * 封装：把对象的属性私有化。同时提供一些可以让外界访问属性的方法。 对外屏蔽细节 可控
    * 继承：使用已存在的类作为基础创建新类。新类可以增加新的数据和功能 又能够使用一些父类的功能
    * 多态：在编译时不确定 在运行时确定类型
* Java语言的特点。简单易学  适合大型项目 多人协作  强类型  千人一面。 利于维护。 平台无关性  Write once, run anywhere 。可靠性 安全性 解决方案多。 开源社区活跃。
* JVM（ Java virtual machine）是运行Java字节码的虚拟机。
在一定程度上解决了传统解释型语言执行效率低的问题。同时又保留了解释型语言可移植的特点
* JDK是Java Development Kit，  java sdk 包括 jre和 一些java命令行工具。 JRE是Java运行时环境
* Oracle JDK 和Open JDK的区别。

协议不同。 Open JDK 是开源的 不完整 。大厂都有自己的Open JDK来避免Oracle JDK收费带来的风险
* Java 和C++的区别。

C++可以直接使用指针操作内存。响应的也比较晦涩难懂。 Java 有自己的内存管理机制 不需要自己释放内存。相对简单还是 灵活性相对较差
* 字符型常量和字符串常量的区别  char 和String  一个单引号 一个双引号   char 2个字节 可以参与运算

## 变量 方法 构造函数
* 装箱 把基本类型转换成 对应的包装类型。 拆箱  包装类型转成基本数据类型  容易NPE
* 成员变量和局部变量的区别
    * 语法形式上： 成员变量属于类 可以被 private public static 等修饰符修饰 而局部变量不行。 但是都可以被final修饰
    * 存储上：     成员变量是对象的一部分。对象存在于堆内存。 局部变量存在于栈内存
    * 生存时间：   局部变量随着方法的调用结束而结束
    * 成员变量     未被显式赋值可以有默认值（有final修饰符的必须显式赋值）。 局部变量必须显式赋值
* 构造方法的作用
完成对类对象的初始化 不显示声明也有默认的构造方法   名称与类名相同 没有返回值 生成类对象时自动执行
    在执行子类的构造方法之前，如果没有用 super 来调用父类特定的构造方法，则会调用父类中**没有参数的构造方法**。
* 静态方法和实例方法
静态方法可以用 类.方法调用 无需创建对象。静态方法在访问本类成员时，只允许访问静态成员(静态成员变量和静态方法)

## 关键字
* this 引用类的当前实例 super 用于从子类访问父类的变量和方法
* final关键字 变量 不可更改 类 不可被继承  方法 不可被继承类修改
* static  
    * 修饰成员变量和成员方法  类名.静态变量名 类名.静态方法名
    * 静态代码块  执行顺序(静态代码块->非静态代码块->构造方法) 静态代码块只会在类加载的时候执行一次
    * 静态内部类(static修饰类的话只能修饰内部类)
    * 静态导包 import static

* final 原理

注：最好先理解java内存模型，后期专门开专题讲解
对于final域，编译器和处理器要遵守两个重排序规则：

1.在构造函数内对一个final域的写入，与随后把这个被构造对象的引用赋值给一个引用变量，这两个操作之间不能重排序。

　　（先写入final变量，后调用该对象引用）

　　原因：编译器会在final域的写之后，插入一个StoreStore屏障

2.初次读一个包含final域的对象的引用，与随后初次读这个final域，这两个操作之间不能重排序。

　　（先读对象的引用，后读final变量）

　　编译器会在读final域操作的前面插入一个LoadLoad屏障
## 重载 and 重写
* 重载和重写的区别
    * 重写：发生在父子类中 方法名和参数列表必须相同。返回值返回小于等于父类 抛出异常范围小于等于父类 访问修饰符范围大于等于父类 private 不能重写
    * 重载： 一个类中。 方法名一样 参数列表不一样 返回值和访问修饰符可以不同 发生在编译时期

## equals hashCode
* 对象的相等比的是内存中存放的内容是否相等。而引用相等比较的是指向的内存地址是否相等
* == 比较的是内存地址 equals() 1 未覆盖equals()方法 等价于==  2. 覆盖 来比较对象的内容是否相等。
    ```java
     String a = new String("ab"); // a 为一个引用
     String b = new String("ab"); // b为另一个引用,对象的内容一样
     String aa = "ab"; // 放在常量池中
     String bb = "ab"; // 从常量池中查找```
     a!=b  aa==bb    a b  aa bb equals 都相等
    ```
* hashCode 和equals
    * hashCode  哈希 散列  目的是为了 快速查找 确定对象位置。
    * hashCode 来检查 重复  向hashSet 里面添加元素 先比较 hashcode  hashcode 一样 在进行equals  (减少equals 次数 来)

    从Object角度看，JVM每new一个Object，它都会将这个Object丢到一个Hash表中去，这样的话，下次做Object的比较或者取这个对象的时候（读取过程），它会根据   对象的HashCode再从Hash表中取这个对象。这样做的目的是提高取对象的效率。若HashCode相同再去调用equal。
    集合要添加新的元素时，先调用这个元素的HashCode方法，就一下子能定位到它应该放置的物理位置上。   
    （1）如果这个位置上没有元素，它就可以直接存储在这个位置上，不用再进行任何比较了；     
    （2）如果这个位置上已经有元素了，就调用它的equals方法与新元素进行比较，相同的话就不存了；    
    （3）不相同的话，也就是发生了Hash key相同导致冲突的情况，那么就在这个Hash key的地方产生一个链表，将所有产生相同HashCode的对象放到这个单链表上去，串在一起（很少出现）。这样一来实际调用equals方法的次数就大大降低了，几乎只需要一两次。

    1. 如果两个对象相同， equals方法一定返回true，并且这两个对象的HashCode一定相同；    
    1. 两个对象的HashCode相同，并不一定表示两个对象就相同，即equals()不一定为true，只能够说明这两个对象在一个散列存储结构中。

## 解决哈希冲突的方法

* 链地址法（拉链法）
* 再哈希法 
* 线行探查法  从该槽位置向后循环遍历hash表，直到找到表中的下一个空槽，并将该元素放入该槽中（会导致相同hash值的元素挨在一起和其他hash值对应的槽被占用）
* 平方探查法
* 双散列函数探查法
* 开放定址法
* 建立公共溢出区

## 基本数据类型
![WX20190422-104914@2x](https://i.loli.net/2019/04/22/5cbd2bf294ec4.png)
## 类型转换
![WX20190422-105235@2x](https://i.loli.net/2019/04/22/5cbd2c8818b32.png)
## Integer
Integer中把-128到127
```java
Integer a = 1000,b=1000;   
Integer c = 100,d=100; 
System.out.println(a==b);  //false
System.out.println(c==d); true
```
//本质 调用valueOf
```java
public static Integer valueOf(int i) {  
    return  i >= 128 || i < -128 ? new Integer(i) : 
    SMALL_VALUES[i + 128];  
}  

private static final Integer[] SMALL_VALUES = new Integer[256];  

static {  
    for (int i = -128; i < 128; i++) {  
        SMALL_VALUES[i + 128] = new Integer(i);  
    }  
}
```
```java
Integer a = new Integer(1000);  
int b = 1000;  
Integer c = new Integer(10);  
Integer d = new Integer(10);  
System.out.println(a == b);   //true  因为自动拆箱 比较的是值
System.out.println(c == d);   //false  ==对象比较的是地址

```

```java
Integer a=NUll;
int b=a  //自动拆箱 NPE       a.vauleof()
```

**Integer和int**

```Java
Integer a = 3;
//等同于
Integer a= Integer.valueOf(3);
```

Integer源码

```java
        static final int low = -128;
        static final int high;
        static final Integer cache[];

        static {
            // high value may be configured by property
            int h = 127;
            String integerCacheHighPropValue =
                sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
            if (integerCacheHighPropValue != null) {
                try {
                    int i = parseInt(integerCacheHighPropValue);
                    i = Math.max(i, 127);
                    // Maximum array size is Integer.MAX_VALUE
                    h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
                } catch( NumberFormatException nfe) {
                    // If the property cannot be parsed into an int, ignore it.
                }
            }
            high = h;    
		public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
          
    public boolean equals(Object obj) {
        if (obj instanceof Integer) {
            return value == ((Integer)obj).intValue();
        }
        return false;
    }
```

Integer默认会缓存`-127~128`范围的数字。 最大值也可以通过JVM数`java.lang.Integer.IntegerCache.high`设置。

```java
        int a=1;
        int b=3;
        System.out.println(a==b);
				//报错
        System.out.println(a.equals(b));
```

* int 和 int 比较   只能使用`==`

  

```java
        Integer a = 123;
        Integer b = 123;
        System.out.println(a==b);
        System.out.println(a.equals(b));
```

* 包装类型 使用 `==` 比较  如果值在-128和127之间，结果为true，否则为false
* 两个包装类在进行`equals`比较时，首先会用`equals`方法判断其类型，如果类型相同，再继续比较值，如果值也相同，则结果为true





```java
        Integer a = 123;
        int b = 23;
        System.out.println(a.equals(b));
        System.out.println(a==b);
```

* Integer 和 int 比较时候。使用`equals` int 会自动装箱
* 使用`==` integer 会自动拆箱



> 对于比较相关问题。 一般只有引用类型 `==` 会产生疑问。 对于引用类型 `==`或者没有重写`equals`方法时  比较的都是 对象的地址。 因为Integer 或者String 有缓存机制。 所以== 在缓存范围内会相等。对于`new`一个对象。地址就不一样了。



## String StringBuilder StringBuffer

* String StringBuilder  StringBuffer
    1. 可变性。    
    String类是使用 final关键词的字符数据来保存字符串 private  final char[]  其他两个都是继承AbstractStringBuilder 里面不带final的
    1. 线程安全性。   
    String因为是不可变的 所以是线程安全的 StringBuffer 加了同步锁 也是线程安全的
    1. 性能    
    每次对String类型的对象进行更改都会生成新的对象。 其他两个都是对自身进行操作。不会生成新的对象
     **综合**    
    少量数据用String  单线程大量用StringBuilder 多线程大量用StringBuffer

* String 对象的两种创建方式

```java
String str1 = "abcd";
String str2 = new String("abcd");
System.out.println(str1==str2);//false
```
这两种不同的创建方法是有差别的，第一种方式是在常量池中拿对象，第二种方式是直接在堆内存空间创建一个新的对象。

注：只要使用new方法，便需要创建新的对象。

* String s1 = new String("abc");这句话创建了几个对象？

```java
        String s1 = new String("abc");// 堆内存的地址值
        String s2 = "abc";
        System.out.println(s1 == s2);// 输出false,因为一个是堆内存，一个是常量池的内存，故两者是不同的。
        System.out.println(s1.equals(s2));// 输出true
```

先有字符串"abc"放入常量池，然后 new 了一份字符串"abc"放入Java堆(字符串常量"abc"在编译期就已经确定放入常量池，而 Java 堆上的"abc"是在运行期初始化阶段才确定)，然后 Java 栈的 str1 指向Java堆上的"abc"。

String 提供的 intern 方法。`String.intern()` 是一个 Native 方法，它的作用是：如果运行时常量池中已经包含一个等于此 String 对象内容的字符串，则返回常量池中该字符串的引用；如果没有，则在常量池中创建与此 String 内容相同的字符串，并返回常量池中创建的字符串的引用。

## 类变量

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfm60t2vlzj30wc0u00xl.jpg)





## 接口 抽象类

* 接口和抽象类有什么区别
    * 相同的：都不能被实例化
    * 不同点：
        * 类可以多实现 只能单继承    
        * 接口强调了是功能的实现 。抽象类强调的是从属关系  
        * 抽象是对类的抽象是一种模板设计，接口是行为的抽象 是一种行为的规范
        * 某些场合下，只靠纯粹的接口不能满足类和类之间的协调，还需要类中表示状态的变量来区别不同的关系。抽象类可以很好的做到这一点
           定义的接口。 但是有些接口 是共同的 和状态不关 可以共享 无需子类分别实现

## 异常体系
* JAVA异常体系：
    Throwable - Error    OutOfMemoryError
              - Exception  -RuntimeException  - NPE  数组越界  算术异常
                           -IOException
    异常能够程序本身处理，但是错误无法被处理

    finally: 无论是否捕获或处理异常,finally都会被执行 ，当在try或者catch块中 遇到return语句时 先执行finally 再return
* transient 修饰不参与序列化
* 获取键盘输入 Scanner  BufferReader （BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
）

## JAVA 网络编程

* InetAddress
* Url
* TCP  `ServerSocket` accept() `Socket`
* UDP 无连接  `DatagramPacket` 数据报 `DatagramSocket` receive()  send()
* HttpClient 几个超时时间配置
```java
RequestConfig config = RequestConfig.custom()
                .setConnectionRequestTimeout(10000)//连接池获取可用连接超时
                .setConnectTimeout(10000)//连接超时
                .setSocketTimeout(30000)//响应超时（读取数据超时）
```
```java
  HttpClientBuilder builder = HttpClientBuilder.create()
                .setDefaultRequestConfig(config)
                .setRetryHandler(new StandardHttpRequestRetryHandler())
                //大多数HTTP连接都被认为是持久的。但是，为了节省服务器资源，连接很少永远保持打开，许多服务器的默认连接超时相当短，例如Apache httpd 2.2及更高版本的5秒。
                //Http客户端池中设置保持未使用连接打开的最长时间
                .setConnectionTimeToLive(1000, TimeUnit.MILLISECONDS)
                //忽略证书
                .setSSLSocketFactory(socketFactory);
```

## JDK自带的工具

* jstack [pid] 查询线程信息
* javap -v 类名  查看字节码
* jad 反编译
* jmap 生成dump信息 查看dump 信息





# Java Web TODO
* Servlet 

接收用户请求 HttpServletRequest 在doGet() 或者doPost中做相应处理 返回HttpServletResponse
init service destroy
一个Servlet 只会有一个实例 所以不是线程安全的
* 转发(Forward) 和重定向(Redirect) 区别
    * 转发:服务器行为  重定向:客户端行为 302 +location
    * 转发 只能跳转 本web应用内页面
    * 地址栏 ：  转发 显示原来的地址
    * 数据共享： 转发页面和转发到的页面可以共享request里面的数据
    * 运用地方：forward:一般用于用户登陆的时候,根据角色转发到相应的模块. redirect:一般用于用户注销登陆时返回主页面和跳转到其它的网站等
    效率： 转发高
* JSP 侧重视图 Servlet侧重逻辑控制

JSP 是在第一次请求的是时候被编译 work/Catalina/
JSP 9大内置对象
request response pageContext session application out config page exception

* Cookie 在客户端 Session在服务器端  因为Http协议是无状态的 会话跟踪 维持会话  现在Token用的比较多




# JAVA IO
!> 同步和异步关注的是**消息通信机制**
* 同步：在发出一个调用时，在没有得到结果之前，该调用就不返回。但是一旦调用返回，就得到返回值了。
* 异步：调用发出之后，这个调用就直接返回了，所以没有返回结果

!> 阻塞和非阻塞：程序在**等待调用结果时的状态。**
* 阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。
* 非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程。
* IO 分类
    * BIO(Block-IO)阻塞IO
    * NIO(Non-Block-IO)非阻塞IO
    * AIO(Asynchronous I/O)异步非阻塞IO
* NIO和IO的区别
    1. IO是面向流的 NIO是面向缓存区的
    2. IO流是阻塞的 NIO流是非阻塞的
    3. NIO有选择器  IO没有

# Spring

## Spring IOE （Inversion of Control）

依赖注入(Dependency Injection)和控制反转(IOC)是从不同的角度的描述的同一件事情，就是指通过引入IOC容器，利用依赖关系注入的方式，实现对象之间的解耦。

Spring IOC 负责创建对象，管理对象（通过依赖注入（DI），装配对象，配置对象，并且管理这些对象的整个生命周期。

所谓的依赖注入，则是，甲方开放接口，在它需要的时候，能够讲乙方传递进来(注入)
所谓的控制反转，甲乙双方不相互依赖，交易活动的进行不依赖于甲乙任何一方，整个活动的进行由第三方负责管理。

ioc的思想最核心的地方在于，**资源不由使用资源的双方管理，而由不使用资源的第三方管理**，这可以带来很多好处。
第一，资源集中管理，实现资源的可配置和易管理。  
第二，降低了使用资源双方的依赖程度，也就是我们说的耦合度。        
**Spring IOC的初始化过程**
![](https://camo.githubusercontent.com/3b07a520440ff631990c027c2437d131fba25efe/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f352f32322f313633383739303365653732633833313f773d37303926683d353626663d706e6726733d34363733)

读取XML资源，并解析，最终注册到Bean Factory中：

* SpringBean注入采用单例时, 跟静态有何分别
    * 可以对bean实现各种拦截(aop,以及通过aop实现的事务和各种操作)
    * 一，便于替换实现。
    * 二，便于单元测试。
    * 三，便于AOP实现。
    * 封装是一个基本特性，static并不满足封装的意义，它其实只是把函数放在一个类里面，并不属于任何一个对象
    * static调用用类名，失去了多态的优越性

## Spring Bean
* spring bean 作用域

![](https://camo.githubusercontent.com/adf4379800711a819fda44c2f478c27469ee5a86/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d392d31372f313138383335322e6a7067)

默认作用域是单例模式 在容器已启动就会自动创建bean对象 有可以配置`lazy-init=”true”`
在第一个使用是创建bean


**Bean的生命周期 initialization 和 destroy**

* 方式一： 实现InitializingBean和DisposableBean接口

```java
public class GiraffeService implements InitializingBean,DisposableBean {
    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("执行InitializingBean接口的afterPropertiesSet方法");
    }
    @Override
    public void destroy() throws Exception {
        System.out.println("执行DisposableBean接口的destroy方法");
    }
}
```
* 方式二： 使用@PostConstruct和@PreDestroy注解

这两个注解均在javax.annotation 包中
```java
public class GiraffeService {
    @PostConstruct
    public void initPostConstruct(){
        System.out.println("执行PostConstruct注解标注的方法");
    }
    @PreDestroy
    public void preDestroy(){
        System.out.println("执行preDestroy注解标注的方法");
    }
}
```
**实现*Aware接口 在Bean中使用Spring框架的一些对象**
```java
public class GiraffeService implements   ApplicationContextAware,
        ApplicationEventPublisherAware, BeanClassLoaderAware, BeanFactoryAware,
        BeanNameAware, EnvironmentAware, ImportAware, ResourceLoaderAware{
         @Override
    public void setBeanClassLoader(ClassLoader classLoader) {
        System.out.println("执行setBeanClassLoader,ClassLoader Name = " + classLoader.getClass().getName());
    }
    @Override
    public void setBeanFactory(BeanFactory beanFactory) throws BeansException {
        System.out.println("执行setBeanFactory,setBeanFactory:: giraffe bean singleton=" +  beanFactory.isSingleton("giraffeService"));
    }
    @Override
    public void setBeanName(String s) {
        System.out.println("执行setBeanName:: Bean Name defined in context="
                + s);
    }
    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        System.out.println("执行setApplicationContext:: Bean Definition Names="
                + Arrays.toString(applicationContext.getBeanDefinitionNames()));
    }
    @Override
    public void setApplicationEventPublisher(ApplicationEventPublisher applicationEventPublisher) {
        System.out.println("执行setApplicationEventPublisher");
    }
    @Override
    public void setEnvironment(Environment environment) {
        System.out.println("执行setEnvironment");
    }
    @Override
    public void setResourceLoader(ResourceLoader resourceLoader) {
        Resource resource = resourceLoader.getResource("classpath:spring-beans.xml");
        System.out.println("执行setResourceLoader:: Resource File Name="
                + resource.getFilename());
    }
    @Override
    public void setImportMetadata(AnnotationMetadata annotationMetadata) {
        System.out.println("执行setImportMetadata");
    }
}
```
**BeanPostProcessor**
上面的*Aware接口是针对某个实现这些接口的Bean定制初始化的过程， Spring同样可以针对容器中的所有Bean，或者某些Bean定制初始化过程，只需提供一个实现BeanPostProcessor接口的类即可。 该接口中包含两个方法，postProcessBeforeInitialization和postProcessAfterInitialization。 postProcessBeforeInitialization方法会在容器中的Bean初始化之前执行， postProcessAfterInitialization方法在容器中的Bean初始化之后执行。
```java
public class CustomerBeanPostProcessor implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("执行BeanPostProcessor的postProcessBeforeInitialization方法,beanName=" + beanName);
        return bean;
    }
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("执行BeanPostProcessor的postProcessAfterInitialization方法,beanName=" + beanName);
        return bean;
    }
}

```

**完整生命周期**
- Bean容器找到配置文件中 Spring Bean 的定义。
- Bean容器利用Java Reflection API创建一个Bean的实例。
- 如果涉及到一些属性值 利用set方法设置一些属性值。
- 如果Bean实现了BeanNameAware接口，调用setBeanName()方法，传入Bean的名字。
- 如果Bean实现了BeanClassLoaderAware接口，调用setBeanClassLoader()方法，传入ClassLoader对象的实例。
- 如果Bean实现了BeanFactoryAware接口，调用setBeanClassLoader()方法，传入ClassLoader对象的实例。
- 与上面的类似，如果实现了其他*Aware接口，就调用相应的方法。
- 如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行- postProcessBeforeInitialization()方法
- 如果Bean实现了InitializingBean接口，执行afterPropertiesSet()方法。
- 如果Bean在配置文件中的定义包含init-method属性，执行指定的方法。
- 如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行postProcessAfterInitialization()方法
- 当要销毁Bean的时候，如果Bean实现了DisposableBean接口，执行destroy()方法。
- 当要销毁Bean的时候，如果Bean在配置文件中的定义包含destroy-method属性，执行指定的方法。
![](https://camo.githubusercontent.com/a3d4415162d30d4659779f6db3717f9a68fd3c97/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d392d31372f353439363430372e6a7067)

**简单版生命周期**
默认情况下，Spring 在读取 xml 文件的时候，就会创建对象。在创建对象的时候先调用构造器，然后调用 init-method 属性值中所指定的方法。对象在被销毁的时候，会调用 destroy-method 属性值中所指定的方法（例如调用Container.destroy()方法的时候）


## Spring 事务


* Spring支持两种方式管理事务
    * 编程式事务管理： 通过Transaction Template手动管理事务，实际应用中很少使用，
    * 配置声明式事务： 推荐使用（代码侵入性最小），实际是通过AOP实现  xml方式 或者 @Transactional 注解

## AOP 面向切面编程
* 通知（Adivce）有5种类型：
    * Before在方法被调用之前调用
    * After在方法完成后调用通知，无论方法是否执行成功
    * After-returning 在方法成功执行之后调用通知
    * After-throwing在方法抛出异常后调用通知
    * Around通知了好、包含了被通知的方法，在被通知的方法调用之前后调用之后执行自定义的行为
* 注解方式 (只是使用的@Aspect 注解 底层还是动态代理的方式)
```java
@Aspect
@Component
public class RestTemplateAop {
    private final Logger logger = LoggerFactory.getLogger(getClass());
    // @Pointcut("@annotation(com.fqgj.common.api.annotations.ParamsValidate)")
    @Pointcut("execution(* org.springframework.web.client.RestTemplate.*(..))")
    private void externalPointCut() {
    }

    @Around("externalPointCut()")
    public Object readAround(ProceedingJoinPoint point) throws Throwable {
        Object[] args = point.getArgs();
        try {
            Object proceed = point.proceed(args);
    }
}
```
* Spring Aop （AOP为Aspect Oriented Programming）实现原理
    静态代理：AspectJ  编译时生成代理类 （静态性能好 但是需要特定的编译器）
    动态代理：JDK动态代理 （反射 以及必须实现接口（因为需要根据接口动态生成类）  Proxy类和 InvocationHandler接口） CGLIB动态代理 （没有实现接口 走这个方式 生成 需要代理类的子类来增强 被final标记的类不能使用此方法）

* JDK Proxy

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.util.Date;

public class LogHandler implements InvocationHandler {
    Object target;  // 被代理的对象，实际的方法执行者

    public LogHandler(Object target) {
        this.target = target;
    }
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        before();
        Object result = method.invoke(target, args);  // 调用 target 的 method 方法
        after();
        return result;  // 返回方法的执行结果
    }
    // 调用invoke方法之前执行
    private void before() {
        System.out.println(String.format("log start time [%s] ", new Date()));
    }
    // 调用invoke方法之后执行
    private void after() {
        System.out.println(String.format("log end time [%s] ", new Date()));
    }
}

```

```java
import proxy.UserService;
import proxy.UserServiceImpl;
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Proxy;

public class Client2 {
    public static void main(String[] args) throws IllegalAccessException, InstantiationException {
        // 设置变量可以保存动态代理类，默认名称以 $Proxy0 格式命名
        // System.getProperties().setProperty("sun.misc.ProxyGenerator.saveGeneratedFiles", "true");
        // 1. 创建被代理的对象，UserService接口的实现类
        UserServiceImpl userServiceImpl = new UserServiceImpl();
        // 2. 获取对应的 ClassLoader
        ClassLoader classLoader = userServiceImpl.getClass().getClassLoader();
        // 3. 获取所有接口的Class，这里的UserServiceImpl只实现了一个接口UserService，
        Class[] interfaces = userServiceImpl.getClass().getInterfaces();
        // 4. 创建一个将传给代理类的调用请求处理器，处理所有的代理对象上的方法调用
        //     这里创建的是一个自定义的日志处理器，须传入实际的执行对象 userServiceImpl
        InvocationHandler logHandler = new LogHandler(userServiceImpl);
        /*
		   5.根据上面提供的信息，创建代理对象 在这个过程中，
               a.JDK会通过根据传入的参数信息动态地在内存中创建和.class 文件等同的字节码
               b.然后根据相应的字节码转换成对应的class，
               c.然后调用newInstance()创建代理实例
		 */
        UserService proxy = (UserService) Proxy.newProxyInstance(classLoader, interfaces, logHandler);
        // 调用代理的方法
        proxy.select();
        proxy.update();
        
        // 保存JDK动态代理生成的代理类，类名保存为 UserServiceProxy
        // ProxyUtils.generateClassFile(userServiceImpl.getClass(), "UserServiceProxy");
    }
}

```
## Spring MVC
* 流程
![](https://camo.githubusercontent.com/6889f839138de730fce5f6a0d64e33258a2cf9b5/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d31302d31312f34393739303238382e6a7067)

（1）客户端（浏览器）发送请求，直接请求到 DispatcherServlet。

（2）DispatcherServlet 根据请求信息调用 HandlerMapping，解析请求对应的 Handler。

（3）解析到对应的 Handler（也就是我们平常说的 Controller 控制器）后，开始由 HandlerAdapter 适配器处理。

（4）HandlerAdapter 会根据 Handler 来调用真正的处理器开处理请求，并处理相应的业务逻辑。

（5）处理器处理完业务后，会返回一个 ModelAndView 对象，Model 是返回的数据对象，View 是个逻辑上的 View。

（6）ViewResolver 会根据逻辑 View 查找实际的 View。

（7）DispaterServlet 把返回的 Model 传给 View（视图渲染）。

（8）把 View 返回给请求者（浏览器）

## Spring Boot
Spring Boot 是Spring开源组织的子项目，主要是简化了使用Spring的难度，省去了繁琐的xml配置，提供了各种启动器方便上手。内置容器

**核心注解**

* 启动类上面的注解是*@SpringBootApplication，它也是 Spring Boot 的核心注解，主要组合包含了以下 3 个注解：
    1. @SpringBootConfiguration：组合了 @Configuration 注解，实现配置文件的功能。
    2. @EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能： @SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })。
    3. @ComponentScan：Spring组件扫描。  
* @Import：用来导入其他配置类。@ImportResource：用来加载xml配置文件。
* 自动配置 替代原来的xml 配置别人的bean @EnableAutoConfiguration, @Configuration @Bean   @Primary 
* @Servcie @Controller  @Component  @Repository 生命自己的bean
* 装配Bean @Autowired 按类型 与@Resource 按名称 @Autowired @Qualifie 两个结合起来可以根据名字和类型注入
* @PropertySource,@Value,@Environment, @ConfigurationProperties 来绑定变量
* @RequestMapping @Controller @RequsetBody @ResponseBody @PathVariable
* @RestControllerAdvice @ExceptionHandler 全局异常处理
* 缓存 数据  查的时候 没有就缓存  更新 删除 都删除缓存 @EnableCaching @CacheConfig  @Cacheable  @CachePut
* 你如何理解 Spring Boot 中的 Starters

Starters可以理解为启动器，它包含了一系列可以集成到应用里面的依赖包，你可以一站式集成 Spring 及其他技术，而不需要到处找示例代码和依赖包。如你想使用 Spring JPA 访问数据库，只要加入 spring-boot-starter-data-jpa 启动器依赖就能使用了。
* CommandLineRunnner\ApplicationRunner启动时指定特定代码
* Spring Boot 如何定义多套不同环境配置？

```
applcation.properties

application-dev.properties

application-test.properties

application-prod.properties
```

* Spring Boot 2.0 新特性
    配置变更
    JDK 版本升级 JDK8
    第三方类库升级
    响应式 Spring 编程支持
    HTTP/2 支持
    配置属性绑定
    更多改进与加强...

* Spring Aop、拦截器、过滤器的区别
    - Filter过滤器：拦截web访问url地址。 这个比拦截器范围广，过滤器是大集合，拦截器是大集合中的小集合。而且任何url是先经过过滤器后才进入拦截器的。
    - Interceptor拦截器：拦截url以action结尾或者没有后缀的,没有后缀拦截器会认为是.action结尾。。 如：struts2拦截器、spring拦截器
    - Spring AOP拦截器：只能拦截Spring管理Bean的访问（业务层Service），就是说执行某个bean容器中方法时进行拦截，而不是对url。

①拦截器是基于java的反射机制的，而过滤器是基于函数回调。    
②拦截器不依赖与servlet容器，过滤器依赖与servlet容器。       
③拦截器只能对action请求起作用，而过滤器则可以对几乎所有的请求起作用。      
④拦截器可以访问action上下文、值栈里的对象，而过滤器不能访问。        
⑤在action的生命周期中，拦截器可以多次被调用，而过滤器只能在容器初始化时被调用一次。         
⑥**拦截器可以获取IOC容器中的各个bean，而过滤器就不行，这点很重要，在拦截器里注入一个service，可以调用业务逻辑。**          
　
过滤器是在请求进入容器后，但请求进入servlet之前进行预处理的。请求结束返回也是，是在servlet处理完后，返回给前端之前。所以过滤器的doFilter(
ServletRequest request, ServletResponse response, FilterChain chain
)的入参是ServletRequest ，而不是httpservletrequest。

拦截器是被包裹在过滤器之中的
**过滤器配置**
```java
    @Order(1)
    @WebFilter(filterName = "testFilter1", urlPatterns = "/*")
    public class TestFilterFirst implements Filter {
        @Override
        public void init(FilterConfig filterConfig) throws ServletException {

        }

        @Override
        public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain)
                throws IOException, ServletException {
            System.out.println("TestFilter1");
            filterChain.doFilter(servletRequest,servletResponse);
        }

        @Override
        public void destroy() {

        }
    }
```
```java
    SpringBootApplication(scanBasePackages = "com.cppba")
    @ServletComponentScan
    public class Application {
        public static void main(String[] args) throws UnknownHostException {
            SpringApplication app = new SpringApplication(Application.class);
            Environment environment = app.run(args).getEnvironment();
        }
    }
```
**拦截器配置**
```java
public class LogCostInterceptor implements HandlerInterceptor {
    long start = System.currentTimeMillis();
    @Override
    public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o) throws Exception {
        start = System.currentTimeMillis();
        return true;
    }
 
    @Override  //渲染视图之前
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
        System.out.println("Interceptor cost="+(System.currentTimeMillis()-start));
    }
 
    @Override //渲染视图之后 一般用于清理资源
    public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
    }
}

```
```java
@Configuration
public class InterceptorConfig extends WebMvcConfigurerAdapter {
 
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LogCostInterceptor()).addPathPatterns("/**");
        super.addInterceptors(registry);
    }
}
```

# MyBatis
优点 半ORM  灵活 SQL可控
* 采用MapperScannerConfigurer，它将会查找类路径下的映射器并自动将它们创建成MapperFactoryBean。
* #{} 和 ${} 的区别

!> \#{}是预编译处理，${}是字符串替换   表名、order by的排序字段作为变量时，使用${}。

* resultMap 映射 实体类和 表 resultType  parameterType
* select LAST_INSERT_ID() 
* 缓存

![20150726164148424](https://i.imgur.com/93nVfYO.png)
* MyBatis编程步骤
    1. 创建SqlSessionFactory
    2. 通过SqlSessionFactory获取SqlSession
    3. 通过SqlSession执行数据库操作
    4. 提交事务
    5. 关闭会话
* 多数据源 多个sqlSessionFactory  采用注解 区分 sqlSessionFactory
* MyBatis和Hibernate的区别
    1. Hibernate完整的实现了对象到数据库结构的映射 帮助我们生产sql，Mybatis仅仅是对结果集映射成了对象 sql要自己写
    2. hibernate 性能优化比较困难
* Mybatis like
    1. 

    ```sql
    <select id="getUsersByName" parameterType="string" resultType="com.buaa.mybatis.po.User">
    SELECT * FROM USER WHERE username LIKE "%"#{name}"%"
    </select>
    ```

    2. MySQL内置函数CONCAT()
    3. Java代码中拼接好 %%
* Mybatis 分页

自带的分页是使用RowBounds对象进行分页 内存分页 不推荐使用
可以使用 直接sql limit 或者 分页插件进行物理分页



# zookeeper
## 是什么
* ZooKeeper是一个开源分布式协调框架 Zk=文件系统+通知机制

## 特点
* Zookeeper数据存在内存中
* ZooKeeper 提供了文件系统和通知机制
* 数据一致性。 每个server保存的都是同一份数据副本
* 更新请求顺序进行。
* 数据更新原子性，一次数据更新要么成功，要么失败
* 实时性。在一定时间范围之内，client能读到最新数据

## 能做什么

0.注册中心      
1.命名服务   
2.配置管理   
3.集群管理   
4.分布式锁  
5.队列管理       
6.服务器节点动态上下线         
7. 数据的发布订阅 watcher
![WX20190318-111342@2x](https://i.imgur.com/2KakJku.png)

## 数据结构
* 类似树
![WX20190318-111042@2x](https://i.imgur.com/sDlM4uw.png)
![WX20190318-160346@2x](https://i.imgur.com/i4yCkS5.png)
* 包含 临时 持久化  顺序 非顺序 Znode（1MB）

## 监听器原理
![WX20190318-160627@2x](https://i.imgur.com/KHE52VE.png)
1. 两个线程 一个线程负责网络连接(connet),一个线程负责监听(listener)
2. 通过 connect 线程将注册的监听事件发送给 Zookeeper。
3. 在 Zookeeper 的注册监听器列表中将注册的监听事件添加到列表中。
4. Zookeeper 监听到有数据或路径变化，就会将这个消息发送给 listener 线程。
5. listener 线程内部调用了 process()方法。

**常见监听**
1. `get path  watch` 监听节点数据变化
2. `ls path  watch` 监听子节点增减变化

## 集群 
* 类似Master/Slave， 一个leader 多个follower，leader负责发起投票、进行决议已经更新系统状态。follower用于接收客户请求返回结果，参与投票。
* 半数以上节点存活 即可工作 >n/2 

## 选举  LeaderElection
目前有5台服务器，每台服务器均没有数据，它们的编号分别是1,2,3,4,5,按编号依次启动，它们的选择举过程如下：

* 服务器1启动，给自己投票，然后发投票信息，由于其它机器还没有启动所以它收不到反馈信息，服务器1的状态一直属于Looking。
* 服务器2启动，给自己投票，同时与之前启动的服务器1交换结果，由于服务器2的编号大所以服务器2胜出，但此时投票数没有大于半数，所以两个服务器的状态依然是LOOKING。
* 服务器3启动，给自己投票，同时与之前启动的服务器1,2交换信息，由于服务器3的编号最大所以服务器3胜出，此时投票数正好大于半数，所以服务器3成为领导者，服务器1,2成为小弟。
* 服务器4启动，给自己投票，同时与之前启动的服务器1,2,3交换信息，尽管服务器4的编号大，但之前服务器3已经胜出，所以服务器4只能成为小弟。
服务器5启动，后面的逻辑同服务器4成为小弟。

## 写数据过程
收到请求发给leader 然后leader发给follower 多数 follower写成功就成功
![WX20190318-161445@2x](https://i.imgur.com/fWTNWrT.png)
* 命令 `create` `set` `get` `ls` `stat` `delete`

## 客户端
* zookeeper的常用客户端有3种，分别是：zookeeper原生的、Apache Curator、开源的zkclient
```Java
ZooKeeper zkClient = new ZooKeeper("192.168.110.100:2181,192.168.110.101:2181", sessionTimeout, new Watcher() { @Override
public void process(WatchedEvent event) {
// 收到事件通知后的回调函数(用户的业务逻辑) 
System.out.println(event.getType() + "--" + event.getPath());
// 再次启动监听 
    try {
        zkClient.getChildren("/", true);
    } catch (Exception e) {
    e.printStackTrace(); 
    }
}
 });

```

# Elasticsearch

## What 什么是Es
Es是一个全文搜索引擎，它可以快速地储存、搜索和分析海量数据。

## Why  为什么要用Es，能解决什么问题，和其他相比有什么好处
!> 全文搜索引擎胜在快速和高效的查询大批量**非结构化**的文本

**Es优点**
1. Es是分布式的。不需要其他组件。
2. Es支持Lucence的接近实时搜索
3. Es采用了GateWay的概念，备份更加简单

**Solr优点**
1. 老牌全文搜索引擎，社区强大and活跃
2. 支持多种格式如 HTML、PDF、DOC、JSON、CSV

**总结**
1. Solr是传统架构、Es是分布式架构 实时搜索效率高
2. 当单纯的对已有数据进行搜索时，Solr更快。
3. 随着数据量的增加，Solr的搜索效率会变得更低，而Elasticsearch却没有明显的变化。

## How Es是如何工作的。如何使用Es
### Es基本概念
* Node 与 Cluster

天然的分布式。一个Es实例为一个Node。一组Node构成一个集群Cluster
* 结合传统数据库对比记忆

MySQL|ElasticSearch
-----|-----
Database(数据库)|Index(索引)
Table(表)|Type(类型)
Row(行)|Document(文档)
Column(列)|Field(字段)
Schema(方案)|Mapping(映射)
Index(索引)|Everthing Indexed by default(所有字段都被索引)
SQL(结构化查询语言)|Query DSL(查询专用语言)

Index里面的单条记录成为Document(文档)。许多Document构成一个Index。 Document可以根据Type进行分组
它是虚拟的逻辑分组，用来过滤 Document。

### 基本命令

```shell
# 新建一个名叫weather的 Index。
curl -X PUT 'localhost:9200/weather'
# 删除Index
curl -X DELETE 'localhost:9200/weather'
# 新增记录 index：accounts  type:person id:1
curl -X PUT 'localhost:9200/accounts/person/1' -d 
'{
  "user": "张三",
  "title": "工程师",
  "desc": "数据库管理"
}' 
# 更新记录 （就是重新发送一次数据）
curl -X PUT 'localhost:9200/accounts/person/1' -d 
'{
    "user" : "张三",
    "title" : "工程师",
    "desc" : "数据库管理，软件开发"
}' 
# 查看记录   pretty=true表示易读的格式
curl 'localhost:9200/accounts/person/1?pretty=true'
# 删除记录 
curl -X DELETE 'localhost:9200/accounts/person/1'
# 查询所有记录  GET  /Index/Type/_search
curl 'localhost:9200/accounts/person/_search'

# 搜索  Match 查询语法  (指定的匹配条件是desc字段里面包含"软件"这个词) form 从什么开始(默认0) size指定条数 （默认10条 ）
curl 'localhost:9200/accounts/person/_search'  -d 
'{
  "query" : { "match" : { "desc" : "软件" }},
  "from": 1,
  "size": 1
}'
# or 多个搜索关键字， Elastic 认为它们是or关系。
curl 'localhost:9200/accounts/person/_search'  -d 
'{
  "query" : { "match" : { "desc" : "软件 系统" }}
}'
# and 
curl 'localhost:9200/accounts/person/_search'  -d 
'{
  "query": {
    "bool": {
      "must": [
        { "match": { "desc": "软件" } },
        { "match": { "desc": "系统" } }
      ]
    }
  }
}'
```

## Java 客户端
ES支持的客户端连接方式
1. REST API ，端口 9200   Java High Level REST Client API  推荐！

```java
<dependency>
    <groupId>org.elasticsearch.client</groupId>
    <artifactId>elasticsearch-rest-high-level-client</artifactId>
    <version>6.7.1</version>
</dependency>
```
2. Transport  tcp连接 端口 9300   官方会逐步抛弃

```java
 <dependency>
        <groupId>org.elasticsearch.client</groupId>
        <artifactId>transport</artifactId>
        <version>6.2.4</version>
 </dependency>
```
JavaApi和ElasticSearch通信的两种方式： 
1. 节点客户端（Node Client）集群中的节点（但不保存数据，不能成为主节点） 知道整个集群状态 这意味着它可以执行 APIs 但少了一个网络跃点。 如果你只需要有少数的、长期持久的对象连接到集群，客户端节点可以更高效
2. 传输客户端（Transport Client）  应用程序和ES集群之前的通讯层。进行节点轮询和集群嗅探 。是外部的 解耦的 适合 大规模集群 推荐！

```java
client = TransportClient.builder().build()
   .addTransportAddress(new InetSocketTransportAddress(InetAddress.getByName("localhost"), 9300));
//搜索
SearchResponse searchResponse = 
    client.prepareSearch("music").setTypes("lyrics").execute().actionGet();
SearchHit[] hits = searchResponse.getHits().getHits();
//插入文档
 StringBuilder json = new StringBuilder("{");
      json.append("\"name\":\""+request.raw().getParameter("name")+"\",");
      json.append("\"artist\":\""+request.raw().getParameter("artist")+"\",");
      json.append("\"year\":"+request.raw().getParameter("year")+",");
      json.append("\"album\":\""+request.raw().getParameter("album")+"\",");
      json.append("\"lyrics\":\""+request.raw().getParameter("lyrics")+"\"}");
 
      IndexRequest indexRequest = new IndexRequest("music", "lyrics",
          UUID.randomUUID().toString());
      indexRequest.source(json.toString());
      IndexResponse esResponse = client.index(indexRequest).actionGet()
```

# Motan

## What

Motan是一套高性能、易于使用的分布式远程服务调用(RPC)框架。

Motan是一套基于java开发的RPC框架，除了常规的点对点调用外，Motan还提供服务治理功能，包括服务节点的自动发现、摘除、高可用和负载均衡等。Motan具有良好的扩展性，主要模块都提供了多种不同的实现，例如支持多种注册中心，支持多种rpc协议等。

## Why   为什么要使用，解决了什么问题。有什么优点。和竞品对比

* 支持通过spring配置方式集成，无需额外编写代码即可为服务提供分布式调用能力。
* 支持集成consul、zookeeper等配置服务组件，提供集群环境的服务发现及治理能力。
* 支持动态自定义负载均衡、跨机房流量调整等高级服务调度能力。
* 基于高并发、高负载场景进行优化，保障生产环境下RPC服务高可用。

!> 与Dubbo 对比。为什么要使用Motan

当时选择Motan 是因为那个时候Dubbo已经停止维护很长时间了。最近一次更新也是在2014年。 (不过 在2017年底 Dubbo重启维护了) 加上Motan是微博开源了。也是经过了大规模生产实践的考验
所以就选择了Motan。 
## How  怎么实现的。 原理。  怎么用 

### 架构概述

Motan中分为服务提供方(RPC Server)，服务调用方(RPC Client)和服务注册中心(Registry)三个角色。

* Server提供服务，向Registry注册自身服务，并向注册中心定期发送心跳汇报状态；
* Client使用服务，需要向注册中心订阅RPC服务，Client根据Registry返回的服务列表，与具体的Sever建立连接，并进行RPC调用。
* 当Server发生变更时，Registry会同步变更，Client感知后会对本地的服务列表作相应调整。

三者的交互关系如下图：

![](https://github.com/weibocom/motan/wiki/media/14612349319195.jpg)

### 代码模块

Motan框架中主要有register、transport、serialize、protocol几个功能模块，各个功能模块都支持通过**SPI**进行扩展，各模块的交互如下图所示：

![](https://github.com/weibocom/motan/wiki/media/14612352579675.jpg)

**register**

支持`Consul`或者`Zookeeper`作为注册中心 
用来和注册中心进行交互，包括注册服务、订阅服务、服务变更通知、服务心跳发送等功能；Server端会在系统初始化时通过register模块注册服务，Client端在系统初始化时会通过register模块订阅到具体提供服务的Server列表，当Server 列表发生变更时也由register模块通知Client。

**protocol**

用来进行RPC服务的描述和RPC服务的配置管理，这一层还可以添加不同功能的filter用来完成统计、并发限制等功能。

**serialize**

将RPC请求中的参数、结果等对象进行序列化与反序列化，即进行对象与字节流的互相转换；默认使用对java更友好的hessian2进行序列化。

**transport**

用来进行远程通信，默认使用**Netty nio**的TCP长链接方式。

**cluster**

Client端使用的模块，cluster是一组可用的Server在**逻辑上的封装**，包含若干可以提供RPC服务的Server，实际请求时会根据不同的高可用与负载均衡策略选择一个可用的Server发起远程调用。

在进行RPC请求时，Client通过代理机制调用cluster模块，cluster根据配置的HA和LoadBalance选出一个可用的Server，通过serialize模块把RPC请求转换为字节流，然后通过transport模块发送到Server端。

![](https://github.com/weibocom/motan/wiki/media/14612385789967.jpg)

Client端订阅Service后，会从Registry中得到能够提供对应Service的一组Server，Client把这一组Server看作一个提供服务的cluster。当cluster中的Server发生变更时，Client端的register模块会通知Client进行更新。

### 处理调用异常

* 业务代码异常
当调用的远程服务出现异常时，Motan会把Server业务中的异常对象抛出到Client代码中，与本地调用逻辑一致。

>注意:如果业务代码中抛出的异常类型为Error而非Exception（如OutOfMemoryError），Motan框架不会直接抛出Error，而是抛出包装了Error的MotanServiceException异常。

* MotanServiceException
使用Motan框架将一个本地调用改为RPC调用后，如果出现网络问题或服务端集群异常等情况，Motan会在Client调用远程服务时抛出MotanServiceException异常，业务方需要自行决定后续处理逻辑。

* MotanFrameworkException
框架异常，比如系统启动、关闭、服务暴露、服务注册等非请求情况下出现问题，Motan会抛出此类异常。

### 负载均衡
* ActiveWeight(缺省)  低并发度优先： referer 的某时刻的 call 数越小优先级越高
* Random
* RoundRobin 轮询
* Consistent 一致性 Hash，相同参数的请求总是发到同一提供者
* ConfigurableWeight 权重可配置的负载均衡策略

### 容错策略

Motan 在集群调用失败时，提供了两种容错方案，并支持自定义扩展。 高可用集群容错策略在Client端生效，因此需在Client端添加配置 目前支持的集群容错策略有：
* Failover 失效切换（缺省） 失败自动切换，当出现失败，重试其它服务器。
* Failfast 快速失败 只发起一次调用，失败立即报错。

### 注册中心与服务发现

### 优雅的停止服务

Motan支持在Consul、ZooKeeper集群环境下优雅的关闭节点，当需要关闭或重启节点时，可以先将待上线节点从集群中摘除，避免直接关闭影响正常请求。

待关闭节点需要调用以下代码，建议通过servlet或业务的管理模块进行该调用。

```java
MotanSwitcherUtil.setSwitcherValue(MotanConstants.REGISTRY_HEARTBEAT_SWITCHER, false)
```
# HBase 

## What  
我们主要用来存储一些 运营商数据  数据量很大。且  非规则
HBase是Apache的Hadoop项目的子项目，是Hadoop Database的简称。

HBase是一个高可靠性、高性能、面向列、可伸缩的分布式存储系统，利用HBase技术可在廉价PC Server上搭建起大规模结构化存储集群。

HBase不同于一般的关系数据库，它是一个适合于**非结构化数据存储**的数据库，HBase**基于列**的而不是基于行的模式。
## Why

hbase表的特性

1、大

hbase表可以存储海量的数据。
2、无模式

mysql表中每一行列的字段是相同，而hbase表中每一行数据可以有截然不同的列。
3、面向列

hbase表中的数据可以有很多个列，后期它就是按照不同的列去存储数据，写入到不同的文件中。
面向列族进行存储数据。
4、稀疏

在hbase表中为null的列并不占用实际的存储空间。
5、数据的多版本

对于hbase表中的数据在进行数据更新的时候，它并没有把之前的结果数据直接删除掉，而是保留数据的多个版本，每一个数据都给一个版本号，这个版本号就是按照我们插入数据的时间戳去确定。
6、数据类型单一

无论是什么类型的数据，最后都被转换成了字节数组存储在hbase表中



## How

### 数据模型

![](https://mmbiz.qpic.cn/mmbiz_png/licvxR9ib9M6AvECce69uqxAGjO2tFu95JpZnOXttW9e3Gm1fvl2FN8xaaQpVxfeFcCApyT8v3S5JfTXmkosGCpA/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

稀疏矩阵、 黑块就是key value

#### RowKey
用来表示唯一一行记录的主键，HBase的数据是按照RowKey的字典顺序进行全局排序的，所有的查询都只能依赖于这一个排序维度。

>通过下面一个例子来说明一下"字典排序"的原理：
RowKey列表{"abc", "a", "bdf", "cdf", "def"}按字典排序后的结果为{"a", "abc", "bdf", "cdf", "defg"}
也就是说，当两个RowKey进行排序时，先对比两个RowKey的第一个字节，如果相同，则对比第二个字节，依次类推...如果在对比到第M个字节时，已经超出了其中一个RowKey的字节长度，那么，短的RowKey要被排在另外一个RowKey的前面。

#### 稀疏矩阵
![](https://mmbiz.qpic.cn/mmbiz_jpg/licvxR9ib9M6AvECce69uqxAGjO2tFu95JwRSQibooSA48r8eibQyfsGnUByzvyVZb5IOynYeicibO3eyFQQsRjJjia3A/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**每一行中，列的组成都是灵活的，行与行之间并不需要遵循相同的列定义**

#### Region

**横向切割**成一个个"子表"，这一个个"子表"就是Region
![](https://mmbiz.qpic.cn/mmbiz_png/licvxR9ib9M6AvECce69uqxAGjO2tFu95JaGQREjtjRR7nnRsD19t6sFf5RUlR7alw6ztacjNU5tDbYsQcxuOKbA/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**Region**是HBase中负载均衡的基本单元，当一个Region增长到一定大小以后，会自动分裂成两个。

#### Column Family

**纵向切割**
![](https://mmbiz.qpic.cn/mmbiz_png/licvxR9ib9M6AvECce69uqxAGjO2tFu95JZzZNC0tZEsNgKY8x3Wt5x0AdHmSIjacvxBQX8DEkJBfjREUibibqdic2w/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### KeyValue


KeyValue的设计不是源自Bigtable，而是要追溯至论文"The log-structured merge-tree(LSM-Tree)"。每一行中的每一列数据，都被包装成独立的拥有特定结构的KeyValue，KeyValue中包含了丰富的自我描述信息:
![](https://mmbiz.qpic.cn/mmbiz_png/licvxR9ib9M6AvECce69uqxAGjO2tFu95JSNy7zECmCYtYYPSoj1ZPK7tVDHVia5mRKDyEj2eTUfuP3U8iar5u6HZw/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
看的出来，KeyValue是支撑"稀疏矩阵"设计的一个关键点：一些Key相同的任意数量的独立KeyValue就可以构成一行数据。但这种设计带来的一个显而易见的缺点：**每一个KeyValue所携带的自我描述信息，会带来显著的数据膨胀。**
# 数据结构和算法

## 排序算法

* 冒泡排序
![849589-20171015223238449-2146169197](https://i.imgur.com/uRIt2KO.gif)


时间复杂度T(n) = O(n2)

```java
public static int[] selectionSort(int[] array) {
        if (array.length == 0)
            return array;
        for (int i = 0; i < array.length; i++) {
            int minIndex = i;
            for (int j = i; j < array.length; j++) {
                if (array[j] < array[minIndex]) //找到最小的数
                    minIndex = j; //将最小数的索引保存
            }
            int temp = array[minIndex];
            array[minIndex] = array[i];
            array[i] = temp;
        }
        return array;
    }
```
* 选择排序
![849589-20171015224719590-1433219824](https://i.imgur.com/V5P9AQD.gif)


时间复杂度T(n) = O(n2) 

```java
 public static int[] selectionSort(int[] array) {
        if (array.length == 0)
            return array;
        for (int i = 0; i < array.length; i++) {
            int minIndex = i;
            for (int j = i; j < array.length; j++) {
                if (array[j] < array[minIndex]) //找到最小的数
                    minIndex = j; //将最小数的索引保存
            }
            int temp = array[minIndex];
            array[minIndex] = array[i];
            array[i] = temp;
        }
        return array;
    }
```

?> * 快速排序算法 TODO


# 设计模式

## 海量数据面试题
hash（散列、杂凑）函数，是将**任意长度的数据**映射到**有限长度的域上**  比如多大文件的MD5、 SHA 长度都是一样的
O(n²)、O(n)、O(1)、O(nlogn) 等？
算法时间复杂度的动机：分析与比较完成同一个任务而设计的不同算法。**预估代码的基本操作执行次数**
!> 海量数据处理的算法思想 大而化小，分而治之（hash映射）

### 海量日志数据，提取出某日访问百度次数最多的那个IP。

ipv4 实际上一个32个位的二进制数。 4个字节。 通常用点分10进制表示
理论上ipv4 可以产生 2^32个ip   每个ip占用4 个字节 那么  所有的ip 共占用 2^32*2^2 =2^34 字节=2^24 kb=2^14mb=2^4GB =16GB
因为有保留地址的缘故 大概有 4GB 。 主要是给一个概念 IP很多。 文件很大。内存加载不了

把这个4GB的大文件 采用流的形式一行一行读IP  通过 对每个IP Hash(ip)%1024 取模 分散到 1024个文件中。 每个文件大概都只有4MB。
然后 对每个 文件 进行hashmap 存储  key为 ip  value 为出现的次数。  取出这1024个文件中 每个文件中最大的。再依据常规的排序算法得到总体上出现次数最多的IP。





# 分布式系统

# Spring Cloud
Spring Cloud 是规范 实现 有  Spring Cloud NetFlix and Spring Cloud Alibaba
![WX20190315-164937@2x](https://i.imgur.com/XQxLikC.png)
![1123](https://i.imgur.com/G2MpfMe.png)
## 注册中心  服务注册和发现

Nacos Discovery、Spring Cloud Netflix Eureka、ZooKeeper 和 Consul （原生）

## 服务消费者
rest （restTemplate）+ribbon 负载均衡 feign
## 配置中心 
Nacos Config 和 Spring Cloud Config  Apollo
## 断路器
Hystrix  Sentinel
## 网关
服务网关是微服务架构中一个不可或缺的部分。通过服务网关统一向外系统提供REST API的过程中，除了具备服务路由、均衡负载功能之外，它还具备了权限控制等功能
Zuul  Spring Cloud GateWay（原生）



# ID生成器 |分布式发号器
**特性**
* 唯一性：确保生成的ID是全网唯一的。
* 有序递增性：确保生成的ID是对于某个用户或者业务是按一定的数字有序递增的。
* 高可用性：确保任何时候都能正确的生成ID。
* 带时间：ID里面包含时间，一眼扫过去就知道哪天的交易。

## 系统时间戳
毫秒数+业务属性+用户属性+随机数+...等参数组合形式来确保ID的唯一性， 缺点是ID的有序性难以保证

## UUID
缺点是它不包含时间、业务数据可读性太差了，而且也不能ID的有序递增。

## 数据库自增ID
这个方案很简单，但最主要的问题在于依赖数据库本身，这就无形增加了对数据库的访问压力和依赖，一旦对单库进行分库分表或者数据迁移就尴尬了。

## 批量生成ID
一次按需批量生成多个ID，每次生成都需要访问数据库，将数据库修改为最大的ID值，并在内存中记录当前值及最大值。
* 优点：避免了每次生成ID都要访问数据库并带来压力，提高性能
* 缺点：属于本地生成策略，存在单点故障，服务重启造成ID不连续

##  Redis生成ID
Redis的所有命令操作都是单线程的，本身提供像 incr 和 increby 这样的自增原子命令，所以能保证生成的 ID 肯定是唯一有序的。
* 优点：不依赖于数据库，灵活方便，且性能优于数据库；数字ID天然排序，对分页或者需要排序的结果很有帮助。
* 缺点：如果系统中没有Redis，还需要引入新的组件，增加系统复杂度；需要编码和配置的工作量比较大。

## Twitter的snowflake算法
![v2-ebae02708fffe6e24fbb3780e0ffab96_hd](https://i.imgur.com/VJxvP5l.jpg)

* 41位的时间序列，精确到毫秒，可以使用69年
* 10位的机器标识，最多支持部署1024个节点
* 12位的序列号，支持每个节点每毫秒产生4096个ID序号，最高位是符号位始终为0。

这种方案性能好，在单机上是递增的，但是由于涉及到分布式环境，每台机器上的时钟不可能完全同步，也许有时候也会出现不是全局递增的情况。

## UidGenerator
UidGenerator是百度开源的分布式ID生成器，基于于snowflake算法的实现

## Leaf

Leaf是美团开源的分布式ID生成器，能保证全局唯一性、趋势递增、单调递增、信息安全，里面也提到了几种分布式方案的对比，但也需要依赖关系数据库、Zookeeper等中间件。

<!-- # 读写分离 分库分表 -->
# 分布式事务

例如做一个服务，最初底下只有一个数据库，用数据库本身的事务来保证数据一致性。随着数据量增长到一定规模，进行了分库，这时数据库的事务就不管用了，如何保证多个库之间的数据一致性呢？

?> **7种解决方案**

## 2PC
2PC有两个角色：事务协调者和事务参与者。具体到数据库的实现来说，每一个数据库就是一个参与者，调用方也就是协调者。2PC是指事务的提交分为两个阶段，如图10-1所示。
* 阶段1：准备阶段。协调者向各个参与者发起询问，说要执行一个事务，各参与者可能回复YES、NO或超时。
* 阶段2：提交阶段。如果所有参与者都回复的是YES，则事务协调者向所有参与者发起事务提交操作，即Commit操作，所有参与者各自执行事务，然后发送ACK。

如果有一个参与者回复的是NO，或者超时了，则事务协调者向所有参与者发起事务回滚操作，所有参与者各自回滚事务，然后发送ACK，如图10-2所示。

![WX20190401-170113@2x](https://i.loli.net/2019/04/01/5ca1d3b567cfe.png ':size=300')

!> 2PC除本身的算法局限外，还有一个使用上的限制，就是它主要用在两个数据库之间（数据库实现了XA协议）。但以支付宝的转账为例，是两个系统之间的转账，而不是底层两个数据库之间直接交互，所以没有办法使用2PC。

## 最终一致性(消息中间件)

!> 实现了消息在发送方的不丢失、在接收方的不重复，联合起来就是消息的不漏不重，严格实现了系统A和系统B的最终一致性。
* 业务方直接实现 +kafaka
![WX20190401-171326@2x](https://i.loli.net/2019/04/01/5ca1d64de14cb.png)
* 基于RocketMQ事务消息
![WX20190401-173451@2x](https://i.loli.net/2019/04/01/5ca1db48c729f.png)
* 人工介入

## TCC
为了解决SOA系统中的分布式事务问题，支付宝提出了TCC。TCC是Try、Confirm、Cancel三个单词的缩写，其实是一个应用层面的2PC协议，Confirm对应2PC中的事务提交操作，Cancel对应2PC中的事务回滚操作，如图10-6所示。

*（1）准备阶段：调用方调用所有服务方提供的Try接口，该阶段各调用方做资源检查和资源锁定，为接下来的阶段2做准备。

*（2）提交阶段：如果所有服务方都返回YES，则进入提交阶段，调用方调用各服务方的Confirm接口，各服务方进行事务提交。如果有一个服务方在阶段1返回NO或者超时了，则调用方调用各服务方的Cancel接口，如图10-7所示。

![WX20190401-173639@2x](https://i.loli.net/2019/04/01/5ca1dbb7840ba.png)
## 事务状态表+调用方重试+接收方幂等

## 对账
## 妥协方案：弱一致性+基于状态的补偿
## 重试+回滚+报警+人工修复

# 分布式Job(Elastic job)

## What

Elastic-Job是一个分布式调度解决方案，由两个相互独立的子项目Elastic-Job-Lite和Elastic-Job-Cloud组成。

Elastic-Job-Lite定位为轻量级无中心化解决方案，使用jar包的形式提供分布式任务的协调服务。

## Why

* 分布式调度协调
* 弹性扩容缩容
* 失效转移
* 错过执行作业重触发
* 作业分片一致性，保证同一分片在分布式环境中仅一个执行实例
* 自诊断并修复分布式不稳定造成的问题
* 支持并行调度
* 支持作业生命周期操作
* 丰富的作业类型
* Spring整合以及命名空间提供
* 运维平台
## How

![](http://elasticjob.io/docs/elastic-job-lite/img/architecture/elastic_job_lite.png)

### 分片概念
任务的分布式执行，需要将一个任务拆分为多个独立的任务项，然后由分布式的服务器分别执行某一个或几个分片项。

例如：有一个遍历数据库某张表的作业，现有2台服务器。为了快速的执行作业，那么每台服务器应执行作业的50%。 为满足此需求，可将作业分成2片，每台服务器执行1片。作业遍历数据的逻辑应为：服务器A遍历ID以奇数结尾的数据；服务器B遍历ID以偶数结尾的数据。 如果分成10片，则作业遍历数据的逻辑应为：每片分到的分片项应为ID%10，而服务器A被分配到分片项0,1,2,3,4；服务器B被分配到分片项5,6,7,8,9，直接的结果就是服务器A遍历ID以0-4结尾的数据；服务器B遍历ID以5-9结尾的数据。

**基于平均分配算法的分片策略，也是默认的分片策略。**

如果分片不能整除，则不能整除的多余分片将依次追加到序号小的服务器。如：  

如果有3台服务器，分成9片，则每台服务器分到的分片是：1=[0,1,2], 2=[3,4,5], 3=[6,7,8]        

如果有3台服务器，分成8片，则每台服务器分到的分片是：1=[0,1,6], 2=[2,3,7], 3=[4,5]       

如果有3台服务器，分成10片，则每台服务器分到的分片是：1=[0,1,2,9], 2=[3,4,5], 3=[6,7,8]        

### 分片项与业务处理解耦

Elastic-Job并不直接提供数据处理的功能，框架只会将分片项分配至各个运行中的作业服务器，开发者需要自行处理分片项与真实数据的对应关系。

###  个性化参数的适用场景

个性化参数即shardingItemParameter，可以和分片项匹配对应关系，用于将分片项的数字转换为更加可读的业务代码。

例如：按照地区水平拆分数据库，数据库A是北京的数据；数据库B是上海的数据；数据库C是广州的数据。 如果仅按照分片项配置，开发者需要了解0表示北京；1表示上海；2表示广州。 合理使用个性化参数可以让代码更可读，如果配置为0=北京,1=上海,2=广州，那么代码中直接使用北京，上海，广州的枚举值即可完成分片项和业务逻辑的对应关系。

# 分布式日志系统
## 概述

ELK 已经成为目前最流行的集中式日志解决方案，它主要是由Beats、Logstash、Elasticsearch、Kibana等组件组成，来共同完成实时日志的收集，存储，展示等一站式的解决方案。本文将会介绍ELK常见的架构以及相关问题解决。

`Filebeat`：Filebeat是一款轻量级，占用服务资源非常少的数据收集引擎，它是ELK家族的新成员，可以代替Logstash作为在应用服务器端的日志收集引擎，支持将收集到的数据输出到Kafka，Redis等队列。        
`Logstash`：数据收集引擎，相较于Filebeat比较重量级，但它集成了大量的插件，支持丰富的数据源收集，对收集的数据可以过滤，分析，格式化日志格式。         
`Elasticsearch`：分布式数据搜索引擎，基于Apache Lucene实现，可集群，提供数据的集中式存储，分析，以及强大的数据搜索和聚合功能。
`Kibana`：数据的可视化平台，通过该web平台可以实时的查看 Elasticsearch 中的相关数据，并提供了丰富的图表统计功能。

## 常见架构

* Logstash作为日志收集器

Logstash比较耗服务器资源，所以会增加应用服务器端的负载压力。

* **Filebeat作为日志收集器**

Filebeat作为应用服务器端的日志收集器(占用资源少)，一般Filebeat会配合Logstash一起使用，这种部署方式也是目前最常用的架构。

* 引入缓存队列的部署架构

这种架构主要是解决大数据量下的日志收集方案，使用缓存队列主要是解决数据安全与均衡Logstash与Elasticsearch负载压力。
![](https://static.oschina.net/uploads/space/2017/1130/131558_J7sa_2842105.png)

# 消息队列
## What 

消息队列中间件是分布式系统中的重要组件，提供消息订阅和发布的能力。主要用于应用解耦，异步消息，流量削峰等问题，实现高性能，高可用，可伸缩和最终一致性架构。目前使用较多的消息队列有
ActiveMQ，RabbitMQ，RocketMQ，Kafka
## Why 
### 消息队列的应用场景
* 应用解耦

![270324-20160730143228325-953675504](/assets/270324-20160730143228325-953675504.png)

假如：在下单时库存系统不能正常使用。也不影响正常下单，因为下单后，订单系统写入消息队列就不再关心其他的后续操作了。实现订单系统与库存系统的应用解耦

* 异步处理

![te](/assets/te.png)

* 流量削峰 xue

流量削锋也是消息队列中的常用场景，**一般在秒杀或团抢活动中使用广泛。**
应用场景：秒杀活动，一般会因为流量过大，导致流量暴增，应用挂掉。为解决这个问题，一般需要在应用前端加入消息队列。
a、可以控制活动的人数
b、可以缓解短时间内高流量压垮应用

![aa1](/assets/aa1.png)
用户的请求，服务器接收后，首先写入消息队列。假如消息队列长度超过最大数量，则直接抛弃用户请求或跳转到错误页面。
秒杀业务根据消息队列中的请求信息，再做后续处理

* 日志处理

日志处理是指将消息队列用在日志处理中，比如Kafka的应用，解决大量日志传输的问题。

* 消息通讯

消息通讯是指，消息队列一般都内置了高效的通信机制，因此也可以用在纯的消息通讯。比如实现点对点消息队列，或者聊天室等


## How
### 消息队列需要解决哪些问题
* Publish/Subscribe 发布订阅是消息中间件的最基本功能，也是相对于传统RPC通信而言。在此不再详述。
* Message Priority 消息优先级
* Message Order 消息有序
* Message Filter 消息过滤
    1. Broker端消息过滤    优点是减少了对于Consumer无用消息的网络传输。缺点是增加了Broker的负担，实现相对复杂。
    2. Consumer端消息过滤  这种过滤方式可由应用完全自定义实现，但是缺点是很多无用的消息要传输到Consumer端。
* Message Persistence 消息持久化
    1. 持久化到数据库
    2. 持久化到KV存储
    3. 文件记录形式持久化，例如Kafka，RocketMQ
    4. 对内存数据做一个持久化镜像
* Message Reliablity 消息可靠性
* Low Latency Messaging 消息低延迟  在消息不堆积情况下，消息到达Broker后，能立刻到达Consumer。
RocketMQ使用长轮询Pull方式，可保证消息非常实时，消息实时性不低于Push。
* At least Once 每个消息必须投递一次。
* Exactly Only Once
    1. 发送消息阶段，不允许发送重复的消息。
    2. 消费消息阶段，不允许消费重复的消息。
* 回溯消费 回溯消费是指Consumer已经消费成功的消息，由于业务上需求需要重新消费，要支持此功能，Broker在向Consumer投递成功消息后，消息仍然需要保留
* 消息堆积 消息中间件的主要功能是异步解耦，还有个重要功能是挡住前端的数据洪峰，保证后端系统的稳定性，这就要求消息中间件具有一定的消息堆积能力，
* 定时消息 定时消息是指消息发到Broker后，不能立刻被Consumer消费，要到特定的时间点或者等待特定的时间后才能被消费。RocketMQ支持定时消息，但是不支持任意时间精度，支持特定的level，例如定时5s，10s，1m等。
* 消息重试 Consumer消费消息失败后，要提供一种重试机制，令消息再消费一次。

### RocketMQ

RocketMQ是阿里开源的消息中间件，它是纯Java开发，具有高吞吐量、高可用性、适合大规模分布式系统应用的特点。RocketMQ思路起源于Kafka，但并不是Kafka的一个Copy，它对消息的可靠传输及事务性做了优化，目前在阿里集团被广泛应用于交易、充值、流计算、消息推送、日志流式处理、binglog分发等场景。

**特点**
* 是一个队列模型的消息中间件，具有高性能、高可靠、高实时、分布式特点。
* Producer、Consumer、队列都可以分布式。
* Producer向一些队列轮流发送消息，队列集合称为Topic，Consumer如果做广播消费，则一个consumer实例消费这个Topic对应的所有队列，如果做集群消费，则多个Consumer实例平均消费这个* * * topic对应的队列集合。
* 能够保证严格的消息顺序
* 提供丰富的消息拉取模式
* 高效的订阅者水平扩展能力
* 实时的消息订阅机制
* 亿级消息堆积能力
* 较少的依赖

![](http://img3.tbcdn.cn/5476e8b07b923/TB18GKUPXXXXXXRXFXXXXXXXXXX)

* Name Server是一个几乎无状态节点，可集群部署，节点之间无任何信息同步。 **路由**  用于给 Producer 和 Consumer 查找 Broker 信息
* Broker分为Master与Slave，一个Master可以对应多个Slave，但是一个Slave只能对应一个Master，每个Broker与Name Server集群中的所有节点建立长连接，定时注册Topic信息到所有Name Server。
* Producer与Name Server集群中的其中一个节点（随机选择）建立长连接，定期从Name Server取Topic路由信息，并向提供Topic服务的Master建立长连接，且定时向Master发送心跳。Producer完全无状态，可集群部署。
* Consumer与Name Server集群中的其中一个节点（随机选择）建立长连接，定期从Name Server取Topic路由信息，并向提供Topic服务的Master、Slave建立长连接，且定时向Master、Slave发送心跳。Consumer既可以从Master订阅消息，也可以从Slave订阅消息，订阅规则由Broker配置决定。
* 消息（Message）就是要传输的信息。一条消息必须有一个主题（Topic），主题可以看做是你的信件要邮寄的地址。一条消息也可以拥有一个可选的标签（Tag）和额处的键值对

**消息消费模式** 
消息消费模式有两种：集群消费（Clustering）和广播消费（Broadcasting）。默认情况下就是集群消费，该模式下一个消费者集群共同消费一个主题的多个队列，一个队列只会被一个消费者消费，如果某个消费者挂掉，分组内其它消费者会接替挂掉的消费者继续消费。而广播消费消息会发给消费者组中的每一个消费者进行消费。

### Kafka
**吞吐量高 一般用在大数据日志处理或对实时性（少量延迟）、可靠性(少量丢数据)要求比较低的场景**

!> Kafka 为什么这么快

Kafka的设计目标是高吞吐量，它比其它消息系统快的原因体现在以下几方面：

1、Kafka操作的是序列文件I / O（序列文件的特征是按顺序写，按顺序读），为保证顺序，Kafka强制点对点的按顺序传递消息，这意味着，一个consumer在消息流（或分区）中只有一个位置。

2、Kafka不保存消息的状态，即消息是否被“消费”。一般的消息系统需要保存消息的状态，并且还需要以随机访问的形式更新消息的状态。而Kafka 的做法是保存Consumer在Topic分区中的位置offset，在offset之前的消息是已被“消费”的，在offset之后则为未“消费”的，并且offset是可以任意移动的，这样就消除了大部分的随机IO。

3、Kafka支持点对点的批量消息传递。

4、Kafka的消息存储在OS pagecache（页缓存，page cache的大小为一页，通常为4K，在Linux读写文件时，它用于缓存文件的逻辑内容，从而加快对磁盘上映像和数据的访问）。

# OAuth2协议

## 应用场景

如：有一个"云冲印"的网站，可以将用户储存在Google的照片，冲印出来。用户为了使用该服务，必须让"云冲印"读取自己储存在Google上的照片。

直接给他们账号密码是不安全的，需要一种安全的授权机制。

## 几种授权模式

* 客户端的授权模式

* 授权码模式

    >（A）用户访问客户端，后者将前者导向认证服务器。  
（B）用户选择是否给予客户端授权。       
（C）假设用户给予授权，认证服务器将用户导向客户端事先指定的"重定向URI"（redirection URI），同时附上一个授权码。     
（D）客户端收到授权码，附上早先的"重定向URI"，向认证服务器申请令牌。这一步是在客户端的后台的服务器上完成的，对用户不可见。   
（E）认证服务器核对了授权码和重定向URI，确认无误后，向客户端发送访问令牌（access token）和更新令牌（refresh token）。 

* 简化模式

简化模式（implicit grant type）不通过第三方应用程序的服务器，直接在浏览器中向认证服务器申请令牌，跳过了"授权码"这个步骤，因此得名。所有步骤在浏览器中完成，令牌对访问者是可见的，且客户端不需要认证。

* 密码模式
* 客户端模式

# nginx
## 是什么 能干什么
Nginx是一款轻量级的Web服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器
## 和其他同类相比优点
Nginx 相对于 Apache 优点：
1) 高并发响应性能非常好，官方 Nginx 处理静态文件并发 5w/s
2) 反向代理性能非常强。（可用于负载均衡）
3) 内存和 cpu 占用率低。（为 Apache 的 1/5-1/10）
4) 对后端服务有健康检查功能。
5) 支持 PHP cgi 方式和 fastcgi 方式。
6) 配置代码简洁且容易上手。 
## 常用命令
```shell
#启动
./nginx 
#检查 nginx.conf配置文件
./nginx -t
#重启
./nginx -s reload
#停止
./nginx -s stop


```
## 配置
默认root 目录  `/usr/share/nginx/html`
```shell
# 全局块
...              
# events块
events {         
   ...
}
# http块
http      
{
    # http全局块
    ...   
    # 虚拟主机server块
    server        
    { 
        # server全局块
        ...       
        # location块
        location [PATTERN]   
        {
            ...
        }
        location [PATTERN] 
        {
            ...
        }
    }
    server
    {
      ...
    }
    # http全局块
    ...     
}


```
1、全局块：配置影响nginx全局的指令。一般有运行nginx服务器的用户组，nginx进程pid存放路径，日志存放路径，配置文件引入，允许生成worker process数等。
2、events块：配置影响nginx服务器或与用户的网络连接。有每个进程的最大连接数，选取哪种事件驱动模型处理连接请求，是否允许同时接受多个网路连接，开启多个网络连接序列化等。

3、http块：可以嵌套多个server，配置代理，缓存，日志定义等绝大多数功能和第三方模块的配置。如文件引入，mime-type定义，日志自定义，是否使用sendfile传输文件，连接超时时间，单连接请求数等。

4、server块：配置虚拟主机的相关参数，一个http中可以有多个server。

5、location块：配置请求的路由，以及各种页面的处理情况。

```shell
########### 每个指令必须有分号结束。#################
#user administrator administrators;  #配置用户或者组，默认为nobody nobody。
#worker_processes 2;  #允许生成的进程数，默认为1
#pid /nginx/pid/nginx.pid;   #指定nginx进程运行文件存放地址
error_log log/error.log debug;  #制定日志路径，级别。这个设置可以放入全局块，http块，server块，级别以此为：debug|info|notice|warn|error|crit|alert|emerg
events {
    accept_mutex on;   #设置网路连接序列化，防止惊群现象发生，默认为on
    multi_accept on;  #设置一个进程是否同时接受多个网络连接，默认为off
    #use epoll;      #事件驱动模型，select|poll|kqueue|epoll|resig|/dev/poll|eventport
    worker_connections  1024;    #最大连接数，默认为512
}
http {
    include       mime.types;   #文件扩展名与文件类型映射表
    default_type  application/octet-stream; #默认文件类型，默认为text/plain
    #access_log off; #取消服务日志    
    log_format myFormat '$remote_addr–$remote_user [$time_local] $request $status $body_bytes_sent $http_referer $http_user_agent $http_x_forwarded_for'; #自定义格式
    access_log log/access.log myFormat;  #combined为日志格式的默认值
    sendfile on;   #允许sendfile方式传输文件，默认为off，可以在http块，server块，location块。
    sendfile_max_chunk 100k;  #每个进程每次调用传输数量不能大于设定的值，默认为0，即不设上限。
    keepalive_timeout 65;  #连接超时时间，默认为75s，可以在http，server，location块。

    # 定义常量
    upstream mysvr {   
      server 127.0.0.1:7878;
      server 192.168.10.121:3333 backup;  #热备
    }
    error_page 404 https://www.baidu.com; #错误页 

    #定义某个负载均衡服务器   
    server {
        keepalive_requests 120; #单连接请求上限次数。
        listen       4545;   #监听端口
        server_name  127.0.0.1;   #监听地址       
        location  ~*^.+$ {       #请求的url过滤，正则匹配，~为区分大小写，~*为不区分大小写。
           #root path;  #根目录
           #index vv.txt;  #设置默认页
           proxy_pass  http://mysvr;  #请求转向mysvr 定义的服务器列表
           deny 127.0.0.1;  #拒绝的ip
           allow 172.18.5.54; #允许的ip           
        } 
    }
} 


```
## 正向代理

正向代理 是一个位于客户端和原始服务器(origin server)之间的服务器，为了从原始服务器取得内容，客户端向代理发送一个请求并指定目标(原始服务器)，然后代理向原始服务器转交请求并将获得的内容返回给客户端。客户端必须要进行一些特别的设置才能使用正向代理。
**用途**
（1）访问原来无法访问的资源，如google
（2）可以做缓存，加速访问资源
（3）对客户端访问授权，上网进行认证
（4）代理可以记录用户访问记录（上网行为管理），对外隐藏

## 反向代理

反向代理（Reverse Proxy）实际运行方式是指以代理服务器来接受internet上的连接请求，然后将**请求转发给内部网络上的服务器**，并将从服务器上得到的结果返回给internet上请求连接的客户端，此时代理服务器对外就表现为一个服务器。
**用途** 
（1）保证内网的安全，可以使用反向代理提供WAF功能，阻止web攻击
（2）负载均衡，通过反向代理服务器来优化网站的负载


## 负载均衡

负载均衡原理及实现
原理：负载均衡是高可用网络基础架构的关键组件，通常用于将工作负载分布到多个服务器来提高网站、应用、数据库或其他服务的性能和可靠性。
一台服务器来做请求处理，把访问到的请求分发到其他几台服务器上，达到服务器减压的效果。（域名只需要指向Nginx服务器IP就可以了）

![WX20190320-164919@2x](https://i.imgur.com/yN5O5XW.png)

**5种方式**
* 1、轮询（默认）
每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。
* 2、weight
指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。
```shell
upstream servername {
    server 192.168.0.14 weight=10;
    server 192.168.0.15 weight=10;
}
```
* 3、ip_hash
每个请求按访问ip的hash结果分配，这样每个访客固定访问一个后端服务器，可以解决session的问题。
```shell
upstream servername {
    ip_hash;
    server 192.168.0.14:88;
    server 192.168.0.15:80;
}
```
* 4、url_hash      
按访问url的hash结果来分配请求，使每个url定向到同一个后端服务器，后端服务器为缓存时比较有效。
例：在upstream中加入hash语句，server语句中不能写入weight等其他的参数，hash_method是使用的hash算法         
```shell
 upstream servername {
    server server1;
    server server2;
    hash $request_uri;
    hash_method crc32;
}
```
* 5、fair 第三方插件
按后端服务器的响应时间来分配请求，响应时间短的优先分配。
```shell
upstream servername {
    server server1;
    server server2;
    fair;
}
```

## 健康检查 检查后端服务是否可用

* 自带方式  `max_fails`  `fail_timeout`
```shell
upstream springboot {
    server 10.3.73.223:8080 max_fails=2 fail_timeout=30s;
    server 10.3.73.223:8090 max_fails=2 fail_timeout=30s;
}
```
* 商用模块 ngx_http_upstream_hc_module `health_check`

```shell
 #Nginx每5s（默认值）就会向dynamic中的每一个服务器发送“/”请求
 location / {
            proxy_pass http://dynamic;
            health_check match=welcome;
        }

```

# Linux
## 目录结构
![](https://camo.githubusercontent.com/5f3d9061e41baf498b2b37c4d80fad87fcf422ff/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f332f313634356631633635363736636166363f773d38323326683d33313526663d706e6726733d3135323236)
* `/bin` 是系统的一些指令。bin为binary的简写主要放置一些系统的必备执行档例如:cat、cp、chmod df、dmesg、gzip、kill、ls、mkdir、more、mount、rm、su、tar等。
* `/sbin`一般是指超级用户指令。主要放置一些系统管理的必备程式例如:cfdisk、dhcpcd、dump、e2fsck、fdisk、halt、ifconfig、ifup、 ifdown、init、insmod、lilo、lsmod、mke2fs、modprobe、quotacheck、reboot、rmmod、 runlevel、shutdown等。
* `/usr/bin`　是你在后期安装的一些软件的运行脚本。主要放置一些应用软体工具的必备执行档例如c++、g++、gcc、chdrv、diff、dig、du、eject、elm、free、gnome*、 gzip、htpasswd、kfm、ktop、last、less、locale、m4、make、man、mcopy、ncftp、 newaliases、nslookup passwd、quota、smb*、wget等。
* `/usr/sbin`   放置一些用户安装的系统管理的必备程式例如:dhcpd、httpd、imap、in.*d、inetd、lpd、named、netconfig、nmbd、samba、sendmail、squid、swap、tcpd、tcpdump等。
* `/etc`:系统管理和配置文件
* `/home`:用户目录
* `/usr`:系统应用程序
* `/opt`:额外安装的应用程序 如tomcat
* `/proc`:虚拟文件系统目录，是系统内存的映射。可直接访问这个目录来获取系统信息
* `/root`:超级管理员
* `/dev`: 存放设备文件
* `/mnt`： 系统管理员安装临时文件系统的安装点，系统提供这个目录是让用户临时挂载其他的文件系统；
* `/boot`： 存放用于系统引导时使用的各种文件；
* `/lib`： 存放着和系统运行相关的库文件 ；
* `/tmp`： 用于存放各种临时文件，是公用的临时文件存储点；
* `/var`： 用于存放运行时需要改变数据的文件，也是某些大文件的溢出区，比方说各种服务的日志文件（系统启动日志等。）等；
* `/lost+found`： 这个目录平时是空的，系统非正常关机而留下“无家可归”的文件（windows下叫什么.chk）就在这里。

## 常用命令
* cd
* mkdir 
* rm  rm -rf  rmdir    `-f 强制 -r 递归`
* mv
* ls
* find 
* cp
* touch
* `ps aux|grep `   `ps -ef` `awk`
* `kill`
* `top`
* `ifconfig`
* `ping`
* `telnet`
* & 后台运行 nohup 忽略退出终端信号
* ssh 
* df -h 查看硬盘空间占用
* shotdown 
* reboot
* snyc scp
* ln -s 软连接 不带 s 硬链接  软连接类似windows快捷方式 指针。硬链接 副本 （修改保持同步）inode 文档信息一样
* sudo  sudo!!
* su
* systemctl

## 解压缩
* tar -zxvf 

-c: 建立压缩档案
-x：解压
-t：查看内容
-r：向压缩归档文件末尾追加文件
-u：更新原压缩包中的文件

这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。

-z：有gzip属性的
-j：有bz2属性的
-Z：有compress属性的
-v：显示所有过程
-O：将文件解开到标准输出

下面的参数-f是必须的

-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。
**压缩** cvf
**解压** xvf

## cat/more/less/tail
* cat： 查看显示文件内容
* more： 可以显示百分比，回车可以向下一行， 空格可以向下一页，b返回q可以退出查看
* less： 可以使用键盘上的PgUp和PgDn向上 和向下翻页，q结束查看
* tail -10 ： 查看文件的后10行，Ctrl+C结束

## vim 
vim 文件------>进入文件----->命令模式------>按i进入编辑模式----->编辑文件 ------->按Esc进入底行模式----->输入:wq/q! （输入wq代表写入内容并退出，即保存；输入q!代表强制退出不保存。）

## 权限
![](https://camo.githubusercontent.com/615d1a5f71d5d9e3370c67fb04f6afbc4374fd5f/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f372f352f313634363935356265373831646161613f773d35383926683d32323826663d706e6726733d3136333630)

读 4  写 2 执行1    属主(owner)，属组(group)和其他用户(other)

文件类型  
d： 代表目录
-： 代表文件
l： 代表软链接（可以认为是window中的快捷方式）

`chmod -R 777 xxx`
`chmod +x xxx`

## top
![WX20190319-102501@2x](https://i.imgur.com/EbJQLez.jpg)

**命令选项**
* c 参考详细命令
* 1 查看多核 多cpu
* t 切换cpu视图
* m 切换memory视图
* b 当前运行的进程
* x 高亮排序 默认 cpu  `shift +<|>`左右移动排序规则
* s 刷新间隔 秒

# Docker  (What、Why 和 How )
## 是什么 能干什么
Build Once, Run Anywhere
容器是一种轻量级的，可移植的，自包含的软件打包技术，使应用程序可以在几乎任何地方以相同的方式运行。
**环境无关性** **动态扩容**

## 和虚拟机对比
隔离程度不同
容器依赖于用户空间。 虚拟机要模拟整个硬件环境 和系统 很大。
![](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170502-1493737075229036266.jpg ':size=500')

Linux 操作系统由内核空间和用户空间组成。内核空间是 `kernel`，Linux 刚启动时会加载 `bootfs` 文件系统，之后 bootfs 会被卸载掉。
用户空间的文件系统是 `rootfs`，包含我们熟悉的 /dev, /proc, /bin 等目录。
对于 base 镜像来说，底层直接用 Host 的 kernel，自己只需要提供 rootfs 就行了。
![](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170423-1492906037945025377.jpg)
所有容器**共享同一个Host OS**，所以体积要比虚拟机小很多，而且启动容器不需要再启动一个操作系统所以容器部署和启动**速度更快**，**开销更小**，**更容易迁移**。

## 原理
* Docker架构
![](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170425-1493117446353024350.jpg)
Docker 采用的是**Client/Server 架构**。客户端向服务器发送请求，服务器负责构建、运行和分发容器。客户端和服务器可以运行在同一个 Host 上，客户端也可以通过 socket 或 REST API 与远程的服务器通信。

容器的底层实现技术。
`cgroup` 和 `namespace` 是最重要的两种技术。`cgroup` 实现资源限额， `namespace` 实现资源隔离。

## 常用命令
* 本地镜像管理
`docker images`
`docker build`
`docker tag`
`docker rmi`
`docker history` 镜像构造历史
* 仓库Registry
`docker pull`
`docker push`
`docker login`

* 容器 
`docekr run ` `docker run -d -p 82:8080 tomcat`   -m -c 
`docekr start/stop/restart pause/unpause`
`docker exec` `docker exec -i -t 31647c341238  bash`
 -it 以交互模式打开  exec 则是在容器中打开新的终端，并且可以启动新的进程。
`docker attach`  
attach 直接进入容器 启动命令 的终端，不会启动新的进程，如果想直接在终端中查看启动命令的输出，用 attach；其他情况使用 exec。
`docker kill`
`docker rm`

`docker ps`
`docker logs`

## DockerFile
构建镜像的两种方式 
1. `docker commit `
2. 编写DockerFile

* 新镜像是从 base 镜像一层一层叠加生成的 **最大的一个好处就是 - 共享资源**
* **Copy-on-Write 特性** 当容器启动时，一个新的可写层被加载到镜像的顶部。
这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”。

![](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170516-1494943681160021117.jpg)
* `FROM scratch`
此镜像是从白手起家，从 0 开始构建。

* `COPY` `ADD` 都是复制  `ADD` 会自动解压
* `RUN`:执行命令并创建新的Image layer，RUN 经常用于安装软件包。
* `CMD`:设置容器启动后默认执行的命令和参数， 但 CMD 能够被 `docker run` 后面跟的命令行参数替换。
* `ENTRYPOINT`:设置容器启动时运行的命令
* `RUN` 为了美观 已经 避免产生过多中间层 `RUN`命令尽量使用&&写成一行并使用\分割
* `WORKDIR` 尽量使用绝对目录
* `ENV`设置环境变量,设置环境变量，环境变量可被后面的指令使用
*  `EXPOSE` 暴露端口 这里暴露端口只是让别人知道暴露了什么端口，不起实际作用。真正起作用是在 run -p 
* `VOLUME` 卷

## 网络
### 单机网络
* none

封闭网络。适用于不需要联网的安全性要求较高的场景。
* host

连接到 host 网络的容器共享 Docker host 的网络栈，容器的网络配置与 host 完全一样
直接使用 Docker host 的网络最大的好处就是性能，如果容器对网络传输效率有较高要求，则可以选择 host 网络。当然不便之处就是牺牲一些灵活性，比如要考虑端口冲突问题，Docker host 上已经使用的端口就不能再用了。
![1](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170622-1498131142416099708.jpg ':size=300')
* brige

`docker network inspect bridge`

`docker network create --driver bridge --subnet 177.22.16.0/24 --gateway 177.22.16.1 my_net2`

只有使用 --subnet 创建的网络才能指定静态 IP。
`docker run -d --network=my_net2 --ip 177.22.16.8 httpd` 

为容器添加一块网卡
` docker network connect my_net2 d6d3b182107d`

## 存储
### 单Host存储
1.由 storage driver 管理的镜像层和容器层。

2.Data Volume。

 |	|bind mount|docker managed volume
 |----|----|---
volume 位置|	可任意指定|	/var/lib/docker/volumes/...
对已有mount point 影响|	隐藏并替换为 volume	|原有数据复制到 volume
是否支持单个文件	|支持	|不支持，只能是目录
权限控制	|可设置为只读，默认为读写权限	|无控制，均为读写权限
移植性	|移植性弱，与 host path 绑定	|移植性强，无需指定 host 目录

## Docker 三剑客
`Docker Compose`：是用来组装多容器应用的工具，可以在 Swarm集群中部署分布式应用。
`Docker Machine`：是支持多平台安装Docker的工具，使用 Docker Machine，可以很方便地在笔记本、云平台及数据中心里安装Docker。
`Docker Swarm`：是Docker社区原生提供的容器集群管理工具。


# Git
## 常用命令

```shell
git config --global user.name "Your Name" 
git config --global user.email "email@example.com" 

git init
git add 
git commit -m 
git push [-f]

git clone 
git branch 
git checkout -b 

git pull = git fetch   +git merge

```
`reset`(重置)和`revert`（提交回滚）区别 
reset是回朔到指定的commit版本（指定commit版本之后的操作都消失了）。       
revert是删除指定的commit操作的内容（指定的版本内容消失，之前和之后commit版本内的操作都保留），但是这个操作也会做了一个commit提交版本。(反向提交)




## GitFlow
* `Master`  最稳定的分支
* `Develop` 主开发分支
* `Feature` 新特性开发。
* `Release` 发布到 test，提测、BUG 修复。
* `HotFix`  线上 BUG 修复。

![20180803135443287](https://i.imgur.com/9wB4wWz.png)

!> 流程

* 新特性开发

接到一个新产品特性 a；
从 develop 分出新分支 feature/a；
在 feature/a 开发特性 a；
完成开发，结束特性 a，代码合并到 develop；
* 提测

从 develop（此时 develop 可能包含多个特性：feature/a、feature/b ...）分出新分支 release/v1.2.0；
在 release/v1.2.0 上修复 QA 测试的 BUG；
完成测试，结束 release/v1.2.0，代码合并到 develop 和 master；

* 修复线上 BUG

从 master 分出新分支 hotfix/v1.2.1；
修复 BUG；
完成 BUG 修复，结束 hotfix/v1.2.1，代码合并到 develop 和 master；


# Apollo 
## What
随着程序功能的日益复杂，程序的配置日益增多：各种功能的开关、参数的配置、服务器的地址……
对程序配置的期望值也越来越高：配置修改后实时生效，灰度发布，分环境、分集群管理配置，完善的权限、审核机制……
在这样的大环境下，传统的通过配置文件、数据库等方式已经越来越无法满足开发人员对配置管理的需求。
Apollo配置中心应运而生！

## Why
* 统一管理不同环境、不同集群的配置
* 配置修改实时生效（热发布）
* 版本发布管理
* 灰度发布
* 权限管理、发布审核、操作审计
* 客户端配置信息监控
* 提供Java和.Net原生客户端
* 提供开放平台API
* 部署简单
## How
### 整体架构
![](https://github.com/ctripcorp/apollo/raw/master/doc/images/overall-architecture.png)
#### ConfigService
* 提供配置获取接口
* 提供配置更新推送接口（基于Http long polling）
    * 服务端使用Spring DeferredResult实现**异步化**，从而大大增加长连接数量
    * 目前使用的tomcat embed默认配置是最多10000个连接（可以调整），使用了4C8G的虚拟机实测可以支撑10000个连接，所以满足需求（一个应用实例只会发起一个**长连接**）。
* 接口服务对象为Apollo客户端

#### Admin Service
* 提供配置管理接口
* 提供配置修改、发布等接口
* 接口服务对象为Portal

#### Meta Server
* Meta Server从Eureka获取Config Service和Admin Service的服务信息，相当于是一个Eureka Client
* 增设一个Meta Server的角色主要是为了封装服务发现的细节，对Portal和Client而言，永远通过一个Http接口获取Admin Service和Config Service的服务信息，而不需要关心背后实际的服务注册和发现组件
* Meta Server只是一个逻辑角色，在部署时和Config Service是在一个JVM进程中的，所以IP、端口和Config Service一致

#### Eureka
* Config Service和Admin Service会向Eureka注册服务，并保持心跳
* 为了简单起见，目前Eureka在部署时和Config Service是在一个JVM进程中的（通过Spring Cloud Netflix）

**为什么采用Eureka作为服务注册中心，而不是传统的Zookeeper、etcd？**

* 完整的Service Registry和Service Discovery实现 经过了Netflix生产环境的考验
* 和SpringCloud 无缝集成。 Eureka还支持在我们应用自身的容器中启动，也就是说我们的应用启动完之后，既充当了Eureka的角色，同时也是服务的提供者。这样就极大的提高了服务的可用性。 减少外部依赖
* 开源

#### Portal
* 提供Web界面供用户管理配置
* 通过Meta Server获取Admin Service服务列表（IP+Port），通过IP+Port访问服务
* 在Portal侧做load balance、错误重试

#### Client

* Apollo提供的客户端程序，为应用提供配置获取、实时更新等功能
* 通过Meta Server获取Config Service服务列表（IP+Port），通过IP+Port访问服务
* 在Client侧做load balance、错误重试

### 服务端设计
#### 配置发布后的实时推送设计
![](https://raw.githubusercontent.com/ctripcorp/apollo/master/doc/images/release-message-notification-design.png) 
![](https://raw.githubusercontent.com/ctripcorp/apollo/master/doc/images/release-message-design.png ':size=500')

**ReleaseMessage**
没有引入mq，采用的线程每秒定时扫描机制

### 客户端设计
![](https://github.com/ctripcorp/apollo/raw/master/doc/images/client-architecture.png)
上图简要描述了Apollo客户端的实现原理：
1. 客户端和服务端保持了一个长连接，从而能第一时间获得配置更新的推送。
2. 客户端还会定时从Apollo配置中心服务端拉取应用的最新配置。
    * 这是一个fallback机制，为了防止推送机制失效导致配置不更新
    * 客户端定时拉取会上报本地版本，所以一般情况下，对于定时拉取的操作，服务端都会返回304 - Not Modified
    * 定时频率默认为每5分钟拉取一次，客户端也可以通过在运行时指定System Property: apollo.refreshInterval来覆盖，单位为分钟。
3. 客户端从Apollo配置中心服务端获取到应用的最新配置后，会保存在内存中
4. 客户端会把从服务端获取到的配置在本地文件系统缓存一份
5. 在遇到服务不可用，或网络不通的时候，依然能从本地恢复配置
6. 应用程序从Apollo客户端获取最新的配置、订阅配置更新通知

#### 配置更新推送实现 | Config Service通知客户端的实现方式
前面提到了Apollo客户端和服务端保持了一个长连接，从而能第一时间获得配置更新的推送。

长连接实际上我们是通过Http Long Polling实现的，具体而言：

* 客户端发起一个Http请求到服务端
* 服务端会保持住这个连接60秒
    * 如果在60秒内有客户端关心的配置变化，被保持住的客户端请求会立即返回，并告知客户端有配置变化的namespace信息，客户端会据此拉取对应namespace的最新配置
    * 如果在60秒内没有客户端关心的配置变化，那么会返回Http状态码304给客户端
* 客户端在收到服务端请求后会立即重新发起连接，回到第一步

考虑到会有数万客户端向服务端发起长连，在服务端我们使用了async servlet(Spring DeferredResult)来服务Http Long Polling请求。

### 和Spring集成的原理
Spring从3.1版本开始增加了ConfigurableEnvironment和PropertySource：
![WX20190409-150047@2x](https://i.loli.net/2019/04/09/5cac43313f2f1.png)

# Sentinel

## What

随着微服务的流行，服务和服务之间的**稳定性**变得越来越重要。Sentinel 是面向分布式服务架构的**轻量级流量控制框架**，主要以流量为切入点，从**流量控制**、**熔断降级**、**系统负载保护**等多个维度来帮助您保护服务的稳定性。

## 基本概念

### 资源

资源是 Sentinel 的关键概念。它可以是 Java 应用程序中的任何内容，只要通过 Sentinel API 定义的代码，就是资源，能够被 Sentinel 保护起来。
Url、RPC服务、甚至一块代码都可以看做是资源。

### 规则

围绕资源的实时状态设定的规则，可以包括流量控制规则、熔断降级规则以及系统保护规则。所有规则可以动态实时调整。

## 主要功能

### 流量控制

流量控制在网络传输中是一个常用的概念，它用于调整网络包的发送数据。然而，从系统稳定性角度考虑，在处理请求的速度上，也有非常多的讲究。**任意时间到来的请求往往是随机不可控的，而系统的处理能力是有限的。我们需要根据系统的处理能力对流量进行控制。**Sentinel 作为一个调配器，可以根据需要把随机的请求调整成合适的形状，如下图所示：

![](https://github.com/alibaba/Sentinel/wiki/image/limitflow.gif)

流量控制有以下几个角度:
* 资源的调用关系，例如资源的调用链路，资源和资源之间的关系；
* 运行指标，例如 QPS、线程池、系统负载等；
* 控制的效果，例如**直接限流**、**冷启动**、**排队**等。

### 熔断降级

除了流量控制以外，降低调用链路中的**不稳定资源**也是 Sentinel 的使命之一。由于调用关系的复杂性，如果调用链路中的某个资源出现了不稳定，最终会导致请求发生堆积。

Sentinel 和 Hystrix 的原则是一致的: 当调用链路中某个资源出现不稳定，**例如，表现为 timeout，异常比例升高的时候，则对这个资源的调用进行限制，并让请求快速失败，避免影响到其它的资源，最终产生雪崩的效果。**


在限制的手段上，Sentinel 和 Hystrix 采取了完全不一样的方法。

Hystrix 通过**线程池**的方式，来对依赖(在我们的概念中对应资源)进行了隔离。这样做的好处是资源和资源之间做到了**最彻底的隔离**。缺点是除了**增加了线程切换的成本**，还需要预先给各个资源做线程池大小的分配。

Sentinel 对这个问题采取了两种手段:

* 通过并发线程数进行限制
和资源池隔离的方法不同，Sentinel 通过限制资源并发线程的数量，来减少不稳定资源对其它资源的影响。这样不但没有线程切换的损耗，也不需要您预先分配线程池的大小。当某个资源出现不稳定的情况下，例如响应时间变长，对资源的直接影响就是会造成线程数的逐步堆积。**当线程数在特定资源上堆积到一定的数量之后，对该资源的新请求就会被拒绝**。堆积的线程完成任务后才开始继续接收请求。

* 通过响应时间对资源进行降级
除了对并发线程数进行控制以外，Sentinel 还可以通过响应时间来快速降级不稳定的资源。**当依赖的资源出现响应时间过长后，所有对该资源的访问都会被直接拒绝，直到过了指定的时间窗口之后才重新恢复。**

### 系统负载保护

Sentinel 同时对系统的维度提供保护。防止雪崩，是系统防护中重要的一环。让系统的入口流量和系统的负载达到一个平衡，保证系统在能力范围之内处理最多的请求。

### 黑白名单  热点参数限流   实时监控  动态规则配置（Zk  Apollo  Nacos）


# 秒杀系统架构

## 什么是秒杀

什么是秒杀？通俗一点讲就是网络商家为促销等目的组织的网上限时抢购活动

## 业务特点

* 瞬时并发量大

秒杀时会有大量用户在同一时间进行抢购，瞬时并发访问量突增 10 倍，甚至 100 倍以上都有。

* 库存量少

一般秒杀活动商品量很少，这就导致了只有极少量用户能成功购买到。

* 业务简单

流程比较简单，一般都是下订单、扣库存、支付订单

## 技术难点

* 现有业务的冲击

秒杀是营销活动中的一种，如果和其他营销活动应用部署在同一服务器上，肯定会对现有其他活动造成冲击，极端情况下可能导致整个电商系统服务宕机

* 直接下订单

下单页面是一个正常的 URL 地址，需要控制在秒杀开始前，不能下订单，只能浏览对应活动商品的信息。简单来说，需要 Disable 订单按钮

* 页面流量突增

秒杀活动开始前后，会有很多用户请求对应商品页面，会造成后台服务器的流量突增，同时对应的网络带宽增加，需要控制商品页面的流量不会对后台服务器、DB、Redis 等组件的造成过大的压力

## 系统架构思想

![WX20190414-134029@2x](https://i.imgur.com/CXN4hS1.png)


* 客户端优化
    * 秒杀页面 页面整体进行静态化，并将页面静态化之后的页面分发到 CDN 边缘节点上，起到压力分散的作用
    * 防止提前下单 disable 按钮
* API 接入层优化
    * 限制用户维度访问频率
    * 限制商品维度访问频率

![WX20190414-134401@2x](https://i.imgur.com/ARKpkyg.png)

秒杀系统核心在于层层过滤，逐渐递减瞬时访问压力，减少最终对数据库的冲击。通过上面流程图就会发现压力最大的地方在哪里？

MQ 排队服务，只要 MQ 排队服务顶住，后面下订单与扣减库存的压力都是自己能控制的，根据数据库的压力，可以定制化创建订单消费者的数量，避免出现消费者数据量过多，导致数据库压力过大或者直接宕机。

库存服务专门为秒杀的商品提供库存管理，实现提前锁定库存，避免超卖的现象。同时，通过超时处理任务发现已抢到商品，但未付款的订单，并在规定付款时间后，处理这些订单，将恢复订单商品对应的库存量

* 不要给数据库太大压力

>　　I：　首先MySQL自身对于高并发的处理性能就会出现问题，一般来说，MySQL的处理性能会随着并发thread上升而上升，但是到了一定的并发度之后会出现明显的拐点，之后一路下降，最终甚至会比单thread的性能还要差。    
　　II： 其次，超卖的根结在于减库存操作是一个事务操作，需要先select，然后insert，最后update -1。最后这个-1操作是不能出现负数的，但是当多用户在有库存的情况下并发操作，出现负数这是无法避免的。        
　　III：最后，当减库存和高并发碰到一起的时候，由于操作的库存数目在同一行，就会出现争抢InnoDB行锁的问题，导致出现互相等待甚至死锁，从而大大降低MySQL的处理性能，最终导致前端页面出现超时异常。

无论是MySQL、Oracle、还是其他关系型数据库，这会造成大量无意义的上下文切换，从而导致资源浪费。假设在网易考拉上有10000个用户对skuId=1的这件商品进行抢购，那么每个时间点仅有一个用户可以获得进入数据库操作的权限，剩下的9999个用户需要等待，待前面的用户完成操作后，会唤醒9999个用户，告诉他们现在可以进入了，9999个用户重新争夺一次，最终又仅有一个用户进入，这就是所谓的上下文切换。在秒杀场景下，这个代价将会非常大，一个显著的表现是CPU负载非常高，但数据库请求的负载却又非常低。
## 总结

!> 核心思想：层层过滤

* 尽量将请求拦截在上游，降低下游的压力

* 充分利用缓存与消息队列，提高请求处理速度以及削峰填谷的作用
# 补充



# Apollo  哨兵  elstic job  motan dubbo elk docker es  hbase jenkins git nginx  

# 亮点 openApi 模板化 自定义注释 统一 gateway入口   适配

# zigbee 终端节点 汇聚节点 自组网  低功耗 通信协议 蓝牙 wifi




# HR

* 试用期时间 和通过试用期的标准