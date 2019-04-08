[TOC]
# Java基础
## 语言特点
* 面向对象和面向过程对比。
    * 面向过程 性能好。
    * 面向对象 容易写出低耦合的代码。利于维护和扩展、复用
* 面向对象的4大特性 封装 继承 多态 抽象
    * 封装：把对象的属性私有化。同时提供一些可以让外界访问属性的方法。 对外屏蔽细节 可控
    * 继承：使用已存在的类作为基础创建新类。新类可以增加新的数据和功能 有能够使用一些父类的功能
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



# 集合相关

## 数组
* System.arraycopy() 和 Arrays.copyOf()方法

copyOf() 内部实际调用了 System.arraycopy() 方法
arraycopy() 需要目标数组，将原数组拷贝到你自己定义的数组里或者原数组，而且可以选择拷贝的起点和长度以及放入新数组中的位置 copyOf() 是系统自动在内部新建一个数组，并返回该数组。

## 集合
* ArrayList 和LinkedList

都是线程不安全的
ArrayList底层结构是数组  LinkedList 是双向链表（
插入和删除是否受元素位置的影响：  ArrayList 受影响o(n)  LinkedList不受影响 o(1)
是否支持快速访问 ArrayList 支持  LinkedList 不支持
内存空间利用  ArrayList的空间浪费 主要是List列表末尾会预留一定的空间  LinkedList的空间浪费主要是 每个元素 都要有直接后继和直接前驱和数据

## Map
* HashMap的底层实现

数组+链表  先通过 hash() 确定元素位置。 如果有元素 判断 新旧元素 hash 和key 是否相同 如果相同覆盖 如果不相同 （此位置建立链表)拉链法解决冲突
1.8之后如果链表长度的大于阀值(默认8) 将链表转化为红黑树（平衡的二叉查找树 解决二叉查找树的缺陷，因为二叉查找树在某些情况下会退化成一个线性结构。） 减少搜索时间
* HashMap 和HashTable的区别

线程安全： HashMap 不安全   HashTable 安全 (内部方法都经过synchronized修饰)
效率:HashMap高一些。 HashTable 基本被淘汰
HashMap支持 一个NULl的Key  ，元素值可以为NULL  so 判断一个key存不存在 应该用containsKey. HashTable不支持NULL 的键值
初始容量 hashMap 默认 16 之后 每次是原来的2倍
* HashSet 的底层就是基于HashMap实现的
* ConcurrentHashMap  分段数组+链表

Segment  分段锁 多线程访问容器里不同数据段的数据，就不会存在锁竞争，提高并发访问率。
到了 JDK1.8 的时候已经摒弃了Segment的概念，而是直接用 Node 数组+链表+红黑树的数据结构来实现，并发控制使用 synchronized 和 CAS 来操作。

ConcurrentHashMap取消了Segment分段锁，采用CAS和synchronized来保证并发安全。数据结构跟HashMap1.8的结构类似，数组+链表/红黑二叉树。
synchronized只锁定当前链表或红黑二叉树的首节点，这样只要hash不冲突，就不会产生并发，效率又提升N倍。
* LinkedHashMap

在HashMap的基础上。增加了一条双向链表，，使得上面的结构可以保持键值对的插入顺序
* Rule 1. 【推荐】底层数据结构是数组的集合，指定集合初始大小

底层数据结构为数组的集合包括 ArrayList，HashMap，HashSet，ArrayDequeue等。

数组有大小限制，当超过容量时，需要进行复制式扩容，新申请一个是原来容量150% or 200%的数组，将原来的内容复制过去，同时浪费了内存与性能。HashMap/HashSet的扩容，还需要所有键值对重新落位，消耗更大。

默认构造函数使用默认的数组大小，比如ArrayList默认大小为10，HashMap为16。因此建议使用ArrayList(int initialCapacity)等构造函数，明确初始化大小。

HashMap/HashSet的初始值还要考虑加载因子:

为了降低哈希冲突的概率(Key的哈希值按数组大小取模后，如果落在同一个数组下标上，将组成一条需要遍历的Entry链)，默认当HashMap中的键值对达到数组大小的75%时，即会触发扩容。因此，如果预估容量是100，即需要设定100/0.75 +1＝135的数组大小。vjkit的MapUtil的Map创建函数封装了该计算。

如果希望加快Key查找的时间，还可以进一步降低加载因子，加大初始大小，以降低哈希冲突的概率。

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

# JVM
* JVM参数设置

-Xms 初始化堆大小
-Xmx 最大堆大小
## 内存结构
* JVM内存模型
![](https://images2015.cnblogs.com/blog/820406/201603/820406-20160326200119386-756216654.png)
* JDK8 Hotshot实现的
![WX20190312-114256@2x](https://i.imgur.com/QQCJpyg.png)

方法区的实现 jdk8之前 是持久代 放到堆中  但是容易引发OOM 后来引入元数据

虚拟机栈
堆 heap     新生代（Eden so s1） 老年代  字符串常量   Eden放不下 YGC   old放不下  YGC          Survivor
元数据  常量池 类元数据  方法元数据 字段 静态属性 方法 常量   方法区  -perm -元数据
本地方法栈 native
程序计数器

## 类加载
* 类加载机制

虚拟机把描述类的数据从class文件加载到内存，并对数据进行校验、转换、解析和初始化。
* **java语言中类型的加载连接以及初始化过程都是在程序运行期间完成的**

这种策略虽然会使类加载时稍微增加一些性能开销，但是会为java应用程序提供高度的灵活性。java里天生就可以动态扩展语言特性就是依赖运行期间动态加载和动态连接这个特点实现的。比如，如果编写一个面向接口的程序，可以等到运行时再指定其具体实现类。
* 类加载过程
![enter image description here](https://mmbiz.qpic.cn/mmbiz_png/hvUCbRic69sAxRovHTCH3yyW1vpic22WVibSBjZicRXsFogpbuwicqugUaxFaIBQnXxwibQ0XTicKxxCVfb0L8sejJkjw/640?wx_fmt=png)
    * 加载
    1. 通过类型的完全限定名，产生一个代表该类型的二进制数据流
    2. 解析这个二进制数据流为方法区内的数据结构
    3. 创建一个表示该类型的java.lang.Class类的实例，作为方法区这个类的各种数据的访问入口。
    * 验证
    为了确保Class文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身的安全。
    * 准备
    准备阶段是正式为类变量分配内存并设置类变量初始值的阶段，这些变量所使用的内存都将在方法区中进行分配。（备注：这时候进行内存分配的仅包括类变量（被static修饰的变量），而不包括实例变量，实例变量将会在对象实例化时随着对象一起分配在Java堆中）。
    初始值通常是数据类型的零值：
         > 对于：public static int value = 123;，那么变量value在准备阶段过后的初始值为0而不是123，这时候尚未开始执行任何java方法，把value赋值为123的动作将在初始化阶段才会被执行。
    一些特殊情况：
    对于：public static final int value = 123;编译时Javac将会为value生成ConstantValue属性，在准备阶段虚拟机就会根据ConstantValue的设置将value赋值为123。
    * 解析
    解析阶段是虚拟机将常量池内的符号引用替换为直接引用的过程。
    * 初始化
    到了初始化阶段，才真正开始执行类中定义的java程序代码（或者说是字节码）。
* 类初始化 
    虚拟机规范严格规定了有且只有五种情况必须立即对类进行“初始化”：
    * 使用new关键字实例化对象的时候、读取或设置一个类的静态字段的时候，已经调用一个类的静态方法的时候。

    * 使用java.lang.reflect包的方法对类进行反射调用的时候，如果类没有初始化，则需要先触发其初始化。

    * 当初始化一个类的时候，如果发现其父类没有被初始化就会先初始化它的父类。

    * 当虚拟机启动的时候，用户需要指定一个要执行的主类（就是包含main()方法的那个类），虚拟机会先初始化这个类；

    * 使用Jdk1.7动态语言支持的时候的一些情况。

    而对于接口，当一个接口在初始化时，并不要求其父接口全部都完成了初始化，只有在真正使用到父接口时（如引用父接口中定义的常量）才会初始化。
    **其他情况不会进行初始化** 
    ①通过子类引用父类静态字段，不会导致子类初始化；
    ②通过数组定义引用类，不会触发此类的初始化
    ③常量在编译阶段会存入调用类的常量池中，本质上并没有直接引用定义常量的类，因此不会触发定义常量的类的初始化

* 类初始化的加载顺序。
    (1) 父类静态代码块(包括静态初始化块，静态属性，但不包括静态方法)
    (2) 子类静态代码块(包括静态初始化块，静态属性，但不包括静态方法 )
    (3) 父类非静态代码块( 包括非静态初始化块，非静态属性 )
    (4) 父类构造函数
    (5) 子类非静态代码块 ( 包括非静态初始化块，非静态属性 )
    (6) 子类构造函数
* 类与类加载器
  对于任意一个类，都需要由加载它的类加载器和这个类本身一同确立其在Java虚拟机中的唯一性。**如果两个类来源于同一个Class文件，只要加载它们的类加载器不同，那么这两个类就必定不相等。**
* 类加载器分类
  * 启动类加载器（Bootstrap）
  C++实现 是虚拟机的一部分 加载 <Java_Runtime_Home>\lib目录中的，或者被-Xbootclasspath参数所指定的路径
  * 其他类加载器 java实现
    * 扩展类加载器 （Extension ClassLoader）
    加载 <Java_Runtime_Home>\lib\ext目录
    * 应用程序类加载器（Application ClassLoader）
    加载用户类路径（ClassPath）上所指定的类库 一般情况下这个就是程序中默认的类加载器。
## 双亲委派模型
* 双亲委派模型
    ![](https://mmbiz.qpic.cn/mmbiz_png/hvUCbRic69sAxRovHTCH3yyW1vpic22WVibsIR7t9TpI4LlxD1hewI5HEy12YhMNtaFohOVOxibnrxCWpXic8Aib9VibQ/640?wx_fmt=png)

    双亲委派模型（Pattern Delegation Model）,要求除了顶层的启动类加载器外，其余的类加载器都应该有自己的**父类加载器**。这里父子关系通常是子类通过**组合**关系而不是继承关系来复用父加载器的代码。

    如果一个类加载器收到了类加载的请求，先把这个**请求委派给父类加载器**去完成（所以所有的加载请求最终都应该传送到顶层的启动类加载器中），只有当父加载器反馈自己无法完成加载请求时，子加载器才会尝试自己去加载。

    使用双亲委派模型来组织类加载器之间的关系，有一个显而易见的好处就是java类随着它的类加载器一起具备了一种带有优先级的**层次**关系。

    **委托机制的意义 — 防止内存中出现多份同样的字节码**

* 能不能自己写个类叫java.lang.System？

答案：不能
解释：为了不让我们写System类，类加载采用委托机制，这样可以保证爸爸们优先，爸爸们能找到的类，儿子就没有机会加载。而System类是Bootstrap加载器加载的，就算自己重写，也总是使用Java系统提供的System，自己写的System类根本没有机会得到加载。

即使我们自定义的类加载器也必须继承自ClassLoader，其loadClass()方法里调用了父类的defineClass()方法，并终究调到preDefineClass()方法，因此我们自定义的类加载器也是不能加载以“java.”开头的java类的。我们继续运行下ClassLoaderTest类，输出以下：
不能自己写以"java."开头的类，其要末不能加载进内存，要末即便你用自定义的类加载器去强行加载，也会收到1个SecurityException。


preDefineClass 不允许java开头的包名被defineClass方法构造

```java
    private ProtectionDomain preDefineClass(String name, ProtectionDomain pd)
{
    // Note:  Checking logic in java.lang.invoke.MemberName.checkForTypeAlias
    // relies on the fact that spoofing is impossible if a class has a name
    // of the form "java.*"
    if ((name != null) && name.startsWith("java.")) {
        throw new SecurityException
            ("Prohibited package name: " +
                name.substring(0, name.lastIndexOf('.')));
    }
}
```
不是hotspot
如果使用的是自定义的虚拟机是可以的 比如android 自定义的
* 自定义类加载器步骤

    （1）继承ClassLoader  
    （2）重写findClass（）方法 
    （3）调用defineClass（）方法 （final修饰）

# 多线程与并发
## 线程
* 一个进程可以产生多个线程。  与进程不同的是 同类的多个线程可以共享同一块内存空间和同一组系统资源 。所以新建线程和线程切换 负担比进程小得多。
   线程(Thread)是进程的一个实体，是CPU调度和分派的基本单位。
* 线程状态：  初始 运行 阻塞 等待 超时等待 终止
* 线程的状态
    ![](https://user-gold-cdn.xitu.io/2018/3/25/1625c6841963873b?w=876&h=492&f=png&s=-1)
    * 新建(NEW)：新创建了一个线程对象
    * 就绪(RUNNABLE) 调用start方法之后
    * 运行(RUNNING) 获取到时间片 执行run方法
    * 阻塞(BLOCKED)
        * 等待阻塞 `object.wait`  进入等待队列  `notify` 进入锁池 
        * 同步阻塞 被其他线程占用。  运行(running)的线程在获取对象的同步锁时，若该同步锁 被别的线程占用，则JVM会把该线程放入锁池(lock pool)中。 `synchronized` 
        * 主动阻塞  主动让出CPU执行权`sleep join  io`
    * 死亡(DEAD)
        run执行结束，or 因异常退出  此状态不可逆转
* 多线程分类
    用户线程（执行具体的任务） 守护线程 （eg:垃圾回收线程）
   Thread setDaemon(true) 为守护线程
* 高并发   指标  响应时间  吞吐量 每秒处理率 qps
* 创建线程的几种方式。
    继承Thread  实现Runnable接口 实现Callable接口 线程池
* 线程优先级具有继承特性比如A线程启动B线程，则B线程的优先级和A是一样的。线程优先级具有随机性也就是说线程优先级高的不一定每一次都先执行完。
     优先级 1 5  10  默认 5
* join() 是阻塞的 “等待该线程终止”，换句话说就是：”当前线程等待子线程的终止“

如果一个线程A执行了thread.join()语句，其含义是：当前线程A等待thread线程终止之后才从thread.join()返回。
* 
    ![WX20190308-151925@2x](https://i.imgur.com/N0BbKOi.png)
    ![WX20190308-1512033@2x](https://i.imgur.com/10qKvBB.png)

  
## Object wait notify 通知机制
* Object wait notify
   ![WX20190308-1031124@2x](https://i.imgur.com/VZwjHqT.png)
    ![WX20190308-103124@2x](https://i.imgur.com/AHjUMY7.png)
   
    wait()  使调用该方法的线程释放共享资源锁，然后从运行状态退出，进入等待队列。知道被再次唤醒
    notify() 随机唤醒等待队列中等待统一共享资源的“一个线程”，并使该线程退出等待队列，进入可运行状态。也就是notify()方法仅通知“一个线程”
* 通知等待的经典范式 

     (调用类的wait和notify方法，就要获取到类的锁。
     ```java
     synchronized(对象) {
       while(条件不满足) {
              对象.wait();
       }
       对应的处理逻辑
    }
    #----------------------
    synchronized(对象) {
       while(条件不满足) {
              对象.wait();
       }
       对应的处理逻辑
    }
     ```
* 当方法wait()被执行后，锁自动被释放，但执行完notify()方法后，锁不会自动释放。必须执行完notify()方法所在的synchronized代码块后才释放。
* 管道输入输出通信流 主要用于线程之间的数据传输 且传输的媒介为内存
  * 面向字节 PipedOutputStream PipedInputStream
  * 面向字符 PipedWriter PipedReader

## ThreadLocal
* ThreadLocal 
    >ThreadLocal，即线程变量，是一个以ThreadLocal对象为键、任意对象为值的存储结构。

    适用于每个线程需要自己独立的实例且该实例需要在多个方法中被使用，也即变量在线程间隔离而在方法或类间共享的场景 ThreadLocal 变量通常被`private static`修饰
    * ThreadLocal 并不解决线程间共享数据的问题
    * ThreadLocal 通过隐式的在不同线程内创建独立实例副本避免了实例线程安全的问题
    * 每个线程持有一个 Map 并维护了 ThreadLocal 对象与具体实例的映射，该 Map 由于只被持有它的线程访问，故不存在线程安全以及锁的问题
    * ThreadMap中数据存储不是用HashMap实现的，而是用Entry[]数组实现，用ThreadLocal的hash值来&长度作为下标，模拟Map。
    * ThreadLocalMap 的 Entry 对 ThreadLocal 的引用为弱引用，避免了 ThreadLocal 对象无法被回收的问题
    * ThreadLocalMap 的 set 方法通过调用 replaceStaleEntry 方法回收键为 null 的 Entry 对象的值（即为具体实例）以及 Entry 对象本身从而防止内存泄漏
    * ThreadLocal 适用于变量在线程间隔离且在方法间共享的场景

* **线程安全性问题存在于实例变量。 访问同一实例的变量 可能会产生线程安全问题**

## volatile
*  volatile 从主存中读取 而不是拷贝到本地内存   保证了可见性 但是无法保证原子性  测试 一个count ++ 100次 主线程++ 新线程-- 最后结果可能不为0
     ```
     取出来count 放入栈顶 0                
    栈顶值+1                            取出来count 放入栈顶  0
    结果返回给count    1                   栈顶值-1
                                     结果返回给count -1
    ```

## sysnchronized
* synchronized  jdk 1.6之后为了 减少 获取锁和释放锁带来的性能消耗引入了偏向锁和轻量级锁
* synchronized 底层原理 “同步块的实现使用了monitorenter和monitorexit指令，而同步方法则是依靠方法修饰符上的ACC_SYNCHRONIZED来完成的”
* synchronized 不具有继承性。

如果父类有一个带synchronized关键字的方法，子类继承并重写了这个方法。
但是同步不能继承，所以还是需要在子类方法中添加synchronized关键字。
synchronized关键字加到static静态方法和synchronized(class)代码块上都是是给Class类上锁，而synchronized关键字加到非static静态方法上是给对象上锁。
* volatile 和synchronized 关键字的区别
   
volatile 用于变量  synchronized修饰方法和代码块
多线程访问volatile不会阻塞 synchronized 可能会发生阻塞
volatile保证的数据的可见性不能保证数据的原子性。 synchronized两者都可以保证
volatile关键字用于解决变量在多个线程之间的可见性，而synchronized关键字解决的是多个线程访问资源的同步性

如果是一些写多读的并发场景 ， 使用 volatile 修饰变量则非常合适。 volatile 一写多读最典型的应用是 CopyOnWriteArrayList

## lock
* 锁 控制对共享资源的方法 。比Synchronized更加灵活

```java
    Lock lock=new ReentrantLock()；
    lock.lock();
    try{
    }finally{
    lock.unlock();
    }
```

最好不要把获取锁的过程写在try语句块中，因为如果在获取锁时发生了异常，异常抛出的同时也会导致锁无法被释放
**lock接口方法**
```java
    void lock() //尝试获取锁，如果锁不可用，则当前线程被禁止进行线程调度 进入休眠状态。知道获取锁
    boolean tryLock()	//只有在调用时才可以获得锁。如果可用，则获取锁定，并立即返回值为true；如果锁不可用，则此方法将立即返回值为false 。
```
* Synchronized 和 ReenTrantLock 的对比
    * 都是可重入锁
    * synchronized 依赖于 JVM 而 ReenTrantLock 依赖于 API（（也就是 API 层面，需要 lock() 和 unlock 方法配合 try/finally 语句块来完成））
    * ReenTrantLock 比 synchronized 增加了一些高级功能 （可设置为公平锁  等待可中断 可实现选择性通知）
    * 性能已不是选择标准
* Java中的锁分类 以下分类不光是指锁的状态，有的指的是锁的特性，有的指的是锁的设计
    * 公平锁/非公平锁      
        是否按照线程申请锁的顺序获取锁，非公平锁的吞吐量大。`Synchronized` 非公平锁 。 `ReentrantLock` 默认非公平锁
    * 可重入锁    
        又名递归锁，是指在同一个线程在外层方法获取锁的时候，在进入内层方法会自动获取锁。好处 一定程度避免死锁   `ReentrantLock` `Synchrozined`
        ```java
        synchronized void setA() throws Exception{
            Thread.sleep(1000);
            setB();
        }    
        synchronized void setB() throws Exception{
            Thread.sleep(1000);
        }
        ```
         当存在父子类继承关系时，子类是可以通过‘可重入锁’调用父类的同步方法
    * 独享锁/共享锁       
        独享锁是指该锁一次只能被一个线程所持有  `ReentrantLock` `Synchronized`
        共享锁是指该锁可被多个线程所持有      ReadWriteLock(读锁共享 写锁独享 并发读效率高 读写 写写 互斥)     
        独享锁与共享锁也是通过AQS来实现的，通过实现不同的方法，来实现独享或者共享。
    * 互斥锁/读写锁     
        上面讲的独享锁/共享锁就是一种广义的说法，互斥锁/读写锁就是具体的实现。
        互斥锁在Java中的具体实现就是`ReentrantLock`
        读写锁在Java中的具体实现就是`ReadWriteLock`
    * 乐观锁/悲观锁    
        悲观的认为，不加锁的并发操作一定会出问题。
        乐观的认为，不加锁的并发操作是没有事情的。        
        从上面的描述我们可以看出，悲观锁适合写操作非常多的场景，乐观锁适合读操作非常多的场景，不加锁会带来大量的性能提升。
        悲观锁在Java中的使用，就是利用各种锁。  
        乐观锁一般会使用版本号或CAS算法实现。
        乐观锁在Java中的使用，是无锁编程，常常采用的是CAS算法，典型的例子就是`java.util.concurrent.atomic`包下面的原子变量类 如: LongAdder，通过CAS自旋实现原子操作的更新。 
        CAS即compare and swap（比较与交换）
        CAS有3个操作数，内存值V，旧的预期值A，要修改的新值B。当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做。。一般情况下是一个自旋操作，即不断的重试 

        * ABA 问题： 如果一个变量V初次读取的时候是A值，并且在准备赋值的时候检查到它仍然是A值，那我们就能说明它的值没有被其他线程修改过了吗？很明显是不能的，因为在这段时间它的值可能被改为其他值，然后又改回A，那CAS操作就会误认为它从来没有被修改过。这个问题被称为CAS操作的 "ABA"问题。

    * 分段锁  
        是一种锁设计 不是一种具体的锁     
    * 偏向锁/轻量级锁/重量级锁      
        指的是锁状态，并且是针对的`Synchronized`
        偏向锁(一段同步代码一直被同一个线程访问该线程自动获取锁，降低获取锁的代价--锁清除--)-->轻量级锁(锁状态为偏向锁时 被另一个线程访问 锁升级为轻量级锁 。 自旋 非阻塞 提高性能 )-->重量级锁
        (自旋到达一定程度仍未获取到锁。锁升级为重量级锁 重量级锁会让其他申请的线程进入阻塞，性能降低。)
    * 自旋锁        
        在Java中，自旋锁是指尝试获取锁的线程不会立即阻塞，而是采用循环的方式去尝试获取锁，这样的好处是减少线程上下文切换的消耗，缺点是循环会消耗CPU。


* AQS(AbstractQueuedSynchronizer）)

AQS核心思想是，如果被请求的共享资源空闲，则将当前请求资源的线程设置为有效的工作线程，并且将共享资源设置为锁定状态。如果被请求的共享资源被占用，那么就需要一套线程阻塞等待以及被唤醒时锁分配的机制，这个机制AQS是用CLH队列锁实现的，即将暂时获取不到锁的线程加入到队列中。
    AQS核心思想是，如果被请求的共享资源空闲，则将当前请求资源的线程设置为有效的工作线程，并且将共享资源设置为锁定状态。如果被请求的共享资源被占用，那么就需要一套线程注释
## 并发工具类
* Semaphore(信号量)-允许多个线程同时访问 
* CountDownLatch(倒计时器) 允许一个或多个线程一直等待，直到其他线程的操作执行完后再执行   

①某一线程在开始运行前等待n个线程执行完毕。将 CountDownLatch 的计数器初始化为n ：`new CountDownLatch(n) `，每当一个任务线程执行完毕，就将计数器减1 `countdownlatch.countDown()`，当计数器的值变为0时，在`CountDownLatch上 await()` 的线程就会被唤醒。一个典型应用场景就是启动一个服务时，主线程需要等待多个组件加载完毕，之后再继续执行。        

②实现多个线程开始执行任务的最大并行性。注意是并行性，不是并发，强调的是多个线程在某一时刻同时开始执行。类似于赛跑，将多个线程放到起点，等待发令枪响，然后同时开跑。做法是初始化一个共享的 `CountDownLatch` 对象，将其计数器初始化为 1 ：`new CountDownLatch(1) `，多个线程在开始执行任务前首先 `coundownlatch.await()`，当主线程调用 countDown() 时，计数器变为0，多个线程同时被唤醒。
    
  
③死锁检测：一个非常方便的使用场景是，你可以使用n个线程访问共享资源，在每次测试阶段的线程数目是不同的，并尝试产生死锁。
*  CyclicBarrier(循环栅栏)

CyclicBarrier 和 CountDownLatch 非常类似，它也可以实现线程间的技术等待，但是它的功能比 CountDownLatch 更加复杂和强大。主要应用场景和 CountDownLatch 类似。

CyclicBarrier 的字面意思是可循环使用（Cyclic）的屏障（Barrier）。它要做的事情是，让一组线程到达一个屏障（也可以叫同步点）时被阻塞，直到最后一个线程到达屏障时，屏障才会开门，所有被屏障拦截的线程才会继续干活。CyclicBarrier默认的构造方法是 `CyclicBarrier(int parties)`，其参数表示屏障拦截的线程数量，每个线程调用`await`方法告诉 CyclicBarrier 我已经到达了屏障，然后当前线程被阻塞。

* CyclicBarrier和CountDownLatch的区别

CountDownLatch是计数器，只能使用一次，而CyclicBarrier的计数器提供reset功能，可以多次使用。但是我不那么认为它们之间的区别仅仅就是这么简单的一点。我们来从jdk作者设计的目的来看，

对于CountDownLatch来说，重点是“一个线程（多个线程）等待”，而其他的N个线程在完成“某件事情”之后，可以终止，也可以等待。而对于CyclicBarrier，重点是多个线程，在任意一个线程没有完成，所有的线程都必须等待。
* happens-before

“两个操作之间具有happens-before关系，并不意味着前一个操作必须要在后一个操作之前执行！happens-before仅仅要求前一个操作（执行的结果）对后一个操作可见，且前一个操作按顺序排在第二个操作之前”
## 原子操作类
*  原子类  AtomicLong 和 LongAdder


## 线程池

* 线程池的好处
    * 降低资源消耗
    * 提高响应速度
    * 提高线程的可管理性
* 创建线程池的几个参数
```java
new  ThreadPoolExecutor(corePoolSize, maximumPoolSize, keepAliveTime,
milliseconds,runnableTaskQueue, handler);
```
    * corePoolSize: 核心线程   cpu密集型 cpu数+1  io密集型 2*cpu数
    * maximumPoolSize: 最大线程
    * runnableTaskQueue:空闲时 线程存货时间
    * TimeUnit:单位
    * runnableTaskQueue：任务队列 LinkedBlockingQueue、ArrayBlockingQueue、PriorityBlockingQueue、SynchronousQueue
    * RejectedExecutionHandler：饱和策略 
        * 直接抛出异常 AbortPolicy 
        * 丢弃队列里最近的一个任务，并执行当前任务 CallerRunsPolicy
        * 不处理 丢弃资源 DiscardOldestPolicy
        * 只有调用者所在的线程运行任务 DiscardPolicy
* 向线程池提交任务
    * execute 不带返回值
    * submit 带返回值 future
* 线程池监控
    * taskCount:线程池需要运行的任务数量
    * completedTaskCount:线程池在运行过程中已经完成的任务数量
    * largestPoolSize: 曾经创建过的最大线程数量
    * getPoolset:线程池的线程数量
    * getActiveCount:活动的线程数
* Executors
    * Executors.newWorkStealingPool: JDK8引入的方法 把CPU数量 设置为默认的并行度
    * Executors.newCachedThreadPool:maximumPoolSize 最大可以至 Integer.MAX_ VAL阻， 是高度可伸缩的线程池 OutOfMemoryError风险
    * Executors.newSingleThreadExecutor:创建个单线程的线程池，相当于单线 程串行执行所有任务 ， 保证接任务的提交顺序依次执行。
    * Executors.newFixedThreadPool : 输入的参数即是固定线程数，既是核心线程
数也是最大线程数 ， 不存在空闲线程，所以 keepAliveTime 等于 O
    
# JAVA IO

* 同步和异步 阻塞 非阻塞
    * 同步和异步关注的是消息通信机制
    * 同步：在发出一个调用时，在没有得到结果之前，该调用就不返回。但是一旦调用返回，就得到返回值了。
    异步：调用发出之后，这个调用就直接返回了，所以没有返回结果

    * 阻塞和非阻塞：程序在等待调用结果时的状态。
    * 阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。
    * 非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程。
    * 阻塞：调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。
    * 非阻塞：在不能立刻得到结果之前。该调用不会阻塞当前线程
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

* 什么是事务
逻辑上的一组操作 要么都执行，要么都不执行
* 事务特性
    * 原子性：事务是最小的执行单位，不允许分割。事务的原子性确保动作要么全部完成要么全部失败
    * 一致性：从一个一致的状态转换到另一个一致状态
    * 隔离性：并发访问数据库时，一个用户的事务不被其他事务所干扰
    * 持久性：一个事务被提交后 数据的改变是持久的
* 带来的问题

**脏读（Dirty read）:** 当一个事务正在访问数据并且对数据进行了修改，而这种修改还没有提交到数据库中，这时另外一个事务也访问了这个数据，然后使用了这个数据。因为这个数据是还没有提交的数据，那么另外一个事务读到的这个数据是“脏数据”，依据“脏数据”所做的操作可能是不正确的。
丢失修改（Lost to modify）: 指在一个事务读取一个数据时，另外一个事务也访问了该数据，那么在第一个事务中修改了这个数据后，第二个事务也修改了这个数据。这样第一个事务内的修改结果就被丢失，因此称为丢失修改。

例如：事务1读取某表中的数据A=20，事务2也读取A=20，事务1修改A=A-1，事务2也修改A=A-1，最终结果A=19，事务1的修改被丢失。

**不可重复读（Unrepeatableread）:** 指在一个事务内多次读同一数据。在这个事务还没有结束时，另一个事务也访问该数据。那么，在第一个事务中的两次读数据之间，由于第二个事务的修改导致第一个事务两次读取的数据可能不太一样。这就发生了在一个事务内两次读到的数据是不一样的情况，因此称为不可重复读。

**幻读（Phantom read）:** 幻读与不可重复读类似。它发生在一个事务（T1）读取了几行数据，接着另一个并发事务（T2）插入了一些数据时。在随后的查询中，第一个事务（T1）就会发现多了一些原本不存在的记录，就好像发生了幻觉一样，所以称为幻读。

* 事务隔离级别

**READ_UNCOMMITTED（未提交读）:** 最低的隔离级别，允许读取尚未提交的数据变更，可能会导致脏读、幻读或不可重复读

**READ_COMMITTED（提交读）:** 允许读取并发事务已经提交的数据，可以阻止脏读，但是幻读或不可重复读仍有可能发生

**REPEATABLE_READ（可重复读）:** 对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，可以阻止脏读和不可重复读，但幻读仍有可能发生。

**SERIALIZABLE（串行）:** 最高的隔离级别，完全服从ACID的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，该级别可以防止脏读、不可重复读以及幻读。但是这将严重影响程序的性能。通常情况下也不会用到该级别。

这里需要注意的是：Mysql 默认采用的 REPEATABLE_READ隔离级别 Oracle 默认采用的 READ_COMMITTED隔离级别.

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
 
    @Override
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
        System.out.println("Interceptor cost="+(System.currentTimeMillis()-start));
    }
 
    @Override
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

!> \#{}是预编译处理，${}是字符串替换

?>  TODO
* resultMap 映射 实体类和 表 resultType  parameterType
* select LAST_INSERT_ID() 
* 缓存
![](https://img-blog.csdn.net/20150726164148424?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
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
# Mysql
## 基础
* insert

```sql
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );

```
* delete

```sql
DELETE FROM table_name [WHERE Clause]
```
* update

```sql
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```
* select

```sql
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]
```
* 关于join时的顺序(小表在前, 大表在后) 节省运算
* DISTINCT
* ORDER BY 
* GROUP BY
* LEFT JOIN（左连接） RIGHT JOIN（右连接）
* ALTER
* TRUNCATE
* utf8 utf8mb4

## 优化/规范
* 使用 ISNULL()来判断是否为 NULL 值。
* 主键索引名为 pk_字段名;唯一索引名为 uk_字段名

## 索引

![](https://camo.githubusercontent.com/0e14b18be2cf0335c3c7d5214aac215f83bf830d/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d31302d322f37303937333438372e6a7067)
* 引擎MyISAM 和INnoDB

MyISAM更适合读密集的表，而InnoDB更适合写密集的的表 MyISAM只支持表级锁
* INnoDB的特点
    * 支持行锁 默认
    * 支持事务
    * 支持外键
    * 支持崩溃后的安全恢复
    * 不支持全文索引
* 表级锁和行级锁对比：

**表级锁：** Mysql中锁定 粒度最大 的一种锁，对当前操作的整张表加锁，实现简单，资源消耗也比较少，加锁快，不会出现死锁。其锁定粒度最大，触发锁冲突的概率最高，并发度最低，MyISAM和 InnoDB引擎都支持表级锁。
**行级锁：** Mysql中锁定 粒度最小 的一种锁，只针对当前操作的行进行加锁。 行级锁能大大减少数据库操作的冲突。其加锁粒度最小，并发度高，但加锁的开销也最大，加锁慢，会出现死锁。

* 索引的好处
    * 索引可以加快数据库的检索速度
    * 表经常进行INSERT/UPDATE/DELETE操作就不要建立索引了，换言之：索引会降低插入、删除、修改等维护任务的速度。
    * 索引需要占物理和数据空间。
    * 了解过索引的最左匹配原则
    * 知道索引的分类：聚集索引和非聚集索引
    * Mysql支持Hash索引和B+树索引两种
* 没有用索引我们是需要遍历双向链表来定位对应的页，现在通过**“目录”**就可以很快地定位到对应的页上了！其实底层结构就是B+树，B+树作为树的一种实现，能够让我们很快地查找出对应的记录。
![](https://user-gold-cdn.xitu.io/2018/7/23/164c6d7a5663f62b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

!> **索引最左匹配原则**

* 索引可以简单如一个列(a)，也可以复杂如多个列(a, b, c, d)，即联合索引。
* 如果是联合索引，那么key也由多个列组成，同时，索引只能用于查找key是否存在（相等），遇到范围查询(>、<、between、like左匹配)等就不能进一步匹配了，后续退化为线性查找。
* 因此，列的排列顺序决定了可命中索引的列数。
* **不需要考虑=、in等的顺序**，mysql会自动优化这些条件的顺序，以匹配尽可能多的索引列。
* 3，尽量选择区分度高的列作为索引，区分度的公式是 COUNT(DISTINCT col) / COUNT(*)。表示字段不重复的比率，比率越大我们扫描的记录数就越少。
* 4，**索引列不能参与计算**，尽量保持列“干净”。比如，FROM_UNIXTIME(create_time) = '2016-06-06' 就不能使用索引，原因很简单，B+树中存储的都是数据表中的字段值，但是进行检索时，需要把所有元素都应用函数才能比较，显然这样的代价太大。所以语句要写成 ： create_time = UNIX_TIMESTAMP('2016-06-06')。
* 5，尽可能的**扩展索引**，不要新建立索引。比如表中已经有了a的索引，现在要加（a,b）的索引，那么只需要修改原来的索引即可。
* 6，单个多列组合索引和多个单列索引的检索查询效果不同，因为在**执行SQL时，MySQL只能使用一个索引**，会从多个单列索引中选择一个限制最为严格的索引。
##锁
![](https://user-gold-cdn.xitu.io/2018/7/23/164c6d7ae44d8ac6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

**表锁**
开销小，加锁快；不会出现死锁；锁定力度大，发生锁冲突概率高，并发度最低
**行锁**
开销大，加锁慢；会出现死锁；锁定粒度小，发生锁冲突的概率低，并发度高

InnoDB只有通过索引条件检索数据才使用行级锁，否则，InnoDB将使用表锁

表锁其实我们程序员是很少关心它的：
在MyISAM存储引擎中，当执行SQL语句的时候是自动加的。
在InnoDB存储引擎中，如果没有使用索引，表锁也是自动加的。
现在我们大多数使用MySQL都是使用InnoDB，InnoDB支持行锁：

**悲观锁** (手动加行锁就行了)
`select * from xxxx for update`
**乐观锁**
`version`
## 切分
* 水平切分

![](https://github.com/CyC2018/CS-Notes/raw/master/docs/notes/pics/63c2909f-0c5f-496f-9fe5-ee9176b31aba.jpg)
水平拆分能够 支持非常大的数据量存储，应用端改造也少，但 分片事务难以解决 ，跨界点Join性能较差，逻辑复杂。《Java工程师修炼之道》的作者推荐 尽量不要对数据进行分片，因为拆分会带来逻辑、部署、运维的各种复杂度 ，一般的数据表在优化得当的情况下支撑千万以下的数据量是没有太大问题的。如果实在要分片，尽量选择客户端分片架构，这样可以减少一次和中间件的网络I/O。
* Sharding 策略
    * 哈希取模：hash(key) % N；
    * 范围：可以是 ID 范围也可以是时间范围；
    * 映射表：使用单独的一个数据库来存储映射关系。
* Sharding 存在的问题
1. 事务问题
使用分布式事务来解决，比如 XA 接口。

2. 连接
可以将原来的连接分解成多个单表查询，然后在用户程序中进行连接。

3. ID 唯一性
使用全局唯一 ID（GUID）
为每个分片指定一个 ID 范围
分布式 ID 生成器 (如 Twitter 的 Snowflake 算法)
* 垂直切分

垂直切分是将一张表按列切分成多个表，通常是按照列的关系密集程度进行切分，也可以利用垂直切分将经常被使用的列和不经常被使用的列切分到不同的表中
![](https://github.com/CyC2018/CS-Notes/raw/master/docs/notes/pics/e130e5b8-b19a-4f1e-b860-223040525cf6.jpg)

* 主从复制 读写分离  云服务提供的能力

* 下面补充一下数据库分片的两种常见方案：

**客户端代理：** 分片逻辑在应用端，封装在jar包中，通过修改或者封装JDBC层来实现。 当当网的 Sharding-JDBC 、阿里的TDDL是两种比较常用的实现。
**中间件代理：** 在应用和数据中间加了一个代理层。分片逻辑统一维护在中间件服务中。 我们现在谈的 Mycat 、360的Atlas、网易的DDB等等都是这种架构的实现。
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
}
```

# Redis
基于内存的高性能数据库  广泛应用于缓存 分布式锁
* Redis 为什么这么快

1、完全基于内存，绝大部分请求是纯粹的内存操作，非常快速。数据存在内存中，类似于HashMap，HashMap的优势就是查找和操作的时间复杂度都是O(1)；

2、数据结构简单，对数据操作也简单，Redis中的数据结构是专门进行设计的；

3、采用单线程，避免了不必要的上下文切换和竞争条件，也不存在多进程或者多线程导致的切换而消耗 CPU，不用去考虑各种锁的问题，不存在加锁释放锁操作，没有因为可能出现死锁而导致的性能消耗；

4、使用多路I/O复用模型，非阻塞IO；

5、使用底层模型不同，它们之间底层实现方式以及与客户端之间通信的应用协议不一样，Redis直接自己构建了VM 机制 ，因为一般的系统调用系统函数的话，会浪费一定的时间去移动和请求；

* 为什么要用缓存\为什么要用Redis
    * 高性能
    假如用户第一次访问数据库中的某些数据。这个过程会比较慢，因为是从硬盘上读取的。将该用户访问的数据存在数缓存中，这样下一次再访问这些数据的时候就可以直接从缓存中获取了。操作缓存就是直接操作内存，所以速度相当快。如果数据库中的对应数据改变的之后，同步改变缓存中相应的数据即可！
    * 高并发
    直接操作缓存能够承受的请求是远远大于直接访问数据库的，所以我们可以考虑把数据库中的部分数据转移到缓存中去，这样用户的一部分请求会直接到缓存这里而不用经过数据库。
* 为什么用Redis 而不是map\guava做缓存

因为Redis是分布式的
* Redis 和Memmcached的区别
    * Redis支持更丰富的数据类型
    * Redis支持数据持久化  快照 or AOF  记录命令
    * Redis有原生的集群模式
    * Memcached是多线程非阻塞IO Redis是单线程非阻塞IO
* String Hash（存储对象） List Set Incr `HSET key field value`

* Redis 过期时间   定期删除 和惰性删除
* Redis 内存淘汰机制 （MySQL里有2000w数据，Redis中只存20w的数据，如何保证Redis中的数据都是热点数据）
    redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略（回收策略）
    redis 提供 6种数据淘汰策略：
        volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰
        volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰
        volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰
        allkeys-lru：当内存不足以容纳新写入数据时，在键空间中，移除最近最少使用的key（这个是最常用的）.
        allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰
        no-eviction：禁止驱逐数据，也就是说当内存不足以容纳新写入数据时，新写入操作会报错。这个应该没人使用吧！
* 缓存雪崩 事前：做好集群  事中：限流 事后：开启Redis持久化机制，尽快恢复缓存集群
* 缓存穿透

简介：一般是黑客故意去请求缓存中不存在的数据，导致所有的请求都落到数据库上，造成数据库短时间内承受大量请求而崩掉。

解决办法： 有很多种方法可以有效地解决缓存穿透问题，最常见的则是采用布隆过滤器（ 不会漏判，但是有一定的误判率（哈希表是精确匹配）），将所有可能存在的数据哈希到一个足够大的bitmap中，一个一定不存在的数据会被 这个bitmap拦截掉，从而避免了对底层存储系统的查询压力。另外也有一个更为简单粗暴的方法（我们采用的就是这种），如果一个查询返回的数据为空（不管是数 据不存在，还是系统故障），我们仍然把这个空结果进行缓存，但它的过期时间会很短，最长不超过五分钟。

* Redis锁的演变  setnx  gatandset Redlock redisson

* JAVA Redis client: Jedis  lettuce  Redisson

# 算法

## 排序算法

* 冒泡排序

![enter image description here](https://images2017.cnblogs.com/blog/849589/201710/849589-20171015223238449-2146169197.gif)

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

![enter image description here](https://images2017.cnblogs.com/blog/849589/201710/849589-20171015224719590-1433219824.gif)

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
* 单例的几种实现方式
    - 饿汉模式
    ```java
        public class MyEagerSingleton {
        private static MyEagerSingleton myEagerSingleton = new MyEagerSingleton();

        private MyEagerSingleton() {

        }

        public static MyEagerSingleton getInstance() {
            return myEagerSingleton;
        }
    }
    ```
    - 懒汉模式  粗暴 方法 synchronized

    ```java
           public class MyLazySingleton {
    private static MyLazySingleton myLazySingleton = null;

    private MyLazySingleton() {

    }

    public synchronized static MyLazySingleton getInstance() {
        if (myLazySingleton == null) {
            myLazySingleton = new MyLazySingleton();
        }
        return myLazySingleton;
    }
    }
    ```

    - 懒汉模式  双重检查锁+ volatile

    ```java
        public class MyLazySingleton02 {
        private static volatile MyLazySingleton02 myLazySingleton02 = null;

        private MyLazySingleton02() {
        }

        public static MyLazySingleton02 getInstance() {
            if (myLazySingleton02 == null) {
                synchronized (MyLazySingleton02.class) {
                    if (myLazySingleton02 == null) {
                        myLazySingleton02 = new MyLazySingleton02();
                    }
                }
            }
            return myLazySingleton02;
        }
    }
    ```

    - 懒汉模式  使用类 初始化一次的特性

    ```java
    public class MyLazySingleton03 {
    private MyLazySingleton03() {

    }
    static class MyLazySingleton03Holder {
        static MyLazySingleton03 myLazySingleton03 = new MyLazySingleton03();
    }
    public static MyLazySingleton03 getInstance() {
        return MyLazySingleton03Holder.myLazySingleton03;
    }

    }
    ```
* 单例 双重检查锁 有问题
    ```java
        public class DoubleCheckedLocking {                      // 1
    private static Instance instance;                    // 2
    public static Instance getInstance() {               // 3
        if (instance == null) {                          // 4:第一次检查
            synchronized (DoubleCheckedLocking.class) {  // 5:加锁
                if (instance == null)                    // 6:第二次检查
                    instance = new Instance();           // 7:问题的根源出在这里
            }                                            // 8
        }                                                // 9
        return instance;                                 // 10
    }                                                    // 11
    }
    ```    
    instance=new Singleton();
        可以拆分为3步

        memory=allocate();//1.分配内存空间
        cotrInstance(memory);//2.初始化对象
        instance=memory;//3. 设置instance指向刚分配的内存地址

        2 3 可能会被重排序
     “双重检查锁定看起来似乎很完美，但这是一个错误的优化！在线程执行到第4行，代码读取到instance不为null时，instance引用的对象有可能还没有完成初始化。”
   
   **解决方案**
    1. volatile 禁止重排序
    2. “基于类初始化的解决方案”

# 计算机网络
* 端口 0-65535  其中0-1023为系统保留端口    http 80、 https 44、 ftp 21 、ssh 22、 zk 2181、 redis 6379

## 网络分层架构
* 7层架构
* TCP/IP 协议分层框架
![WX20190319-144015@2x](https://i.imgur.com/WZzWGeK.png)
    * 应用层
    HTTP、FTP、SMTP
    * 传输层
    最典型的传输层协议是 UDP 和 TCP。 UDP 只是在 IP 数据包上增加端口等部分 信息 ， 是**面向无连接**的，是不可靠传输，多用于视频通信、电话会议等(即 使少一帧数据也无妨)。与之相反 ， **TCP 是面向连接的。所谓面向连接** ， 是 一种端到端间通过失败重传机制建立的可靠数据传输方式，给人感觉是有一 条固定的通路承载着数据的可靠传输。
    * 网络层
    IP数据包 TTL  IP寻址  ` ICMP`  MTU最大传输单元
         * IP等级  IP位置  
        Class A 10.0.0.0-10.255.255.255  
        Class B 172.16.0.0-172.31.255.255  
        Class C 192.168.0.0-192.168.255.255
    * 链路层
    MAC地址

总结一下 ， 程序在发送消息时，应用层接既定的协议打包数据 ， 随后由传输层加 上双方的端口 号 ，由网络层加上双方的 IP 地址，由链路层加上双方的 MAC 地址 ， 并 将数据拆分成数据帧 ， 经过多个路由器 和 网关后 ， 至lj达目标机器。简而言之 ， 就是按
**“端口→ IP 地址→ MAC 地址 ”** 这样的路径进行数据的封装和发送 ， 解包的时候反过 来操作即可。
![WX20190319-144749@2x](https://i.imgur.com/J8xstaY.png)

## TCP UDP
* TCP 
    * TCP 是面向连接的。（就好像打电话一样，通话前需要先拨号建立连接，通话结束后要挂机释放连接）；
    每一条 TCP 连接只能有两个端点，每一条TCP连接只能是点对点的（一对一）；
    * TCP 提供可靠交付的服务。通过TCP连接传送的数据，无差错、不丢失、不重复、并且按序到达；
    * TCP 提供全双工通信。TCP 允许通信双方的应用进程在任何时候都能发送数据。TCP 连接的两端都设有发送缓存和接收缓存，用来临时存放双方通信的数据；
    * 面向字节流。TCP 中的“流”（Stream）指的是流入进程或从进程流出的字节序列。“面向字节流”的含义是：虽然应用程序和 TCP 的交互是一次一个数据块（大小不等），但 TCP 把应用程序交下来的数据仅仅看成是一连串的无结构的字节流。
* UDP
    * UDP 是无连接的；
    * UDP 使用尽最大努力交付，即不保证可靠交付，因此主机不需要维持复杂的链接状态（这里面有许多参数）；
    * UDP 是面向报文的；
    * UDP 没有拥塞控制，因此网络出现拥塞不会使源主机的发送速率降低（对实时应用很有用，如 直播，实时视频会议等）；
    * UDP 支持一对一、一对多、多对一和多对多的交互通信；
    * UDP 的首部开销小，只有8个字节，比TCP的20个字节的首部要短。
* TCP和UDP的区别

![](https://camo.githubusercontent.com/409f705f6df8c77c7166e543eefa07c40511a28a/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f342f31392f313632646235653937653961396530313f696d61676556696577322f302f772f313238302f682f3936302f666f726d61742f776562702f69676e6f72652d6572726f722f31)
* TCP三次握手

![](https://camo.githubusercontent.com/484f4f39a6e6bb5f4d6cda6709bff7196a23161b/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f352f382f313633336531323733393635343166313f773d38363426683d34333926663d706e6726733d323236303935)
简单示意图： TCP三次握手

客户端–发送带有 SYN 标志的数据包–一次握手–服务端
服务端–发送带有 SYN/ACK 标志的数据包–二次握手–客户端
客户端–发送带有带有 ACK 标志的数据包–三次握手–服务端
**三次握手就能确认双发收发功能都正常**
* TCP4次挥手
![](https://camo.githubusercontent.com/ae140718e064bf5f444224c9da3cdc2b8cd9f9a6/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f352f382f313633336531363736653261633061333f773d35303026683d33343026663d6a70656726733d3133343036)
断开一个 TCP 连接则需要“四次挥手”：

1.客户端-发送一个 FIN，用来关闭客户端到服务器的数据传送
2.服务器-收到这个 FIN，它发回一 个 ACK，确认序号为收到的序号加1 。和 SYN 一样，一个 FIN 将占用一个序号
3.服务器-关闭与客户端的连接，发送一个FIN给客户端
4.客户端-发回 ACK 报文确认，并将确认序号设置为收到序号加1
* TCP 协议如何保证可靠传输
    * 应用数据被分割成 TCP 认为最适合发送的数据块。
    * TCP 给发送的每一个包进行编号，接收方对数据包进行排序，把有序数据传送给应用层。
    * **校验和：** TCP 将保持它首部和数据的检验和。这是一个端到端的检验和，目的是检测数据在传输过程中的任何变化。如果收到段的检验和有差错，TCP 将丢弃这个报文段和不确认收到此报文段。
    * TCP 的接收端会丢弃重复的数据。
    * **流量控制：** TCP 连接的每一方都有固定大小的缓冲空间，TCP的接收端只允许发送端发送接收端缓冲区能接纳的数据。当接收方来不及处理发送方的数据，能提示发送方降低发送的速率，防止包丢失。TCP 使用的流量控制协议是可变大小的滑动窗口协议。 （TCP 利用滑动窗口实现流量控制）
    * **拥塞控制：** 当网络拥塞时，减少数据的发送。
    * **停止等待协议** 也是为了实现可靠传输的，它的基本原理就是每发完一个分组就停止发送，等待对方确认。在收到确认后再发下一个分组。
    * **超时重传：** 当 TCP 发出一个段后，它启动一个定时器，等待目的端确认收到这个报文段。如果不能及时收到一个确认，将重发这个报文段。
* 滑动窗口
    * TCP 利用滑动窗口实现流量控制的机制。
    * 滑动窗口（Sliding window）是一种流量控制技术。早期的网络通信中，通信双方不会考虑网络的拥挤情况直接发送数据。由于大家不知道网络拥塞状况，同时发送数据，导致中间节点阻塞掉包，谁也发不了数据，所以就有了滑动窗口机制来解决此问题。
    * TCP 中采用滑动窗口来进行传输控制，滑动窗口的大小意味着接收方还有多大的缓冲区可以用于接收数据。发送方可以通过滑动窗口的大小来确定应该发送多少字节的数据。当滑动窗口为 0 时，发送方一般不能再发送数据报，但有两种情况除外，一种情况是可以发送紧急数据，例如，允许用户终止在远端机上的运行进程。另一种情况是发送方可以发送一个 1 字节的数据报来通知接收方重新声明它希望接收的下一字节及发送方的滑动窗口大小。

## HTTP
* get 和 post
    * get 一般是从服务器获取资源 post 一般是提交数据
    * get 是在url ？后 以name=value &分割的形式传递数据  post是在body中
    * get 受到url长度限制（这个限制并不是http协议规定的 而是不同的浏览器限制不同 1kb 2kb ）
    * get 数据会显示在地址栏上。 敏感数据可以用post

    **深层次：**
    GET和POST本质上就是TCP链接，并无差别。但是由于HTTP的规定和浏览器/服务器的限制，导致他们在应用过程中体现出一些不同。
    GET产生一个TCP数据包；POST产生两个TCP数据包。
    restful 各自语义不要混用。
* Https 协议原理：

https=http+ssl/tls . 证书相当与 公私钥

https 使用了 对称加密和非对称加密相结合的方式。

请求一个https的网站，会返回一个 证书 证书包含公钥和过期时间 等信息。

客户端需要对 公钥进行认证。采用CA根证书的公钥 解密出网站的公钥 然后验签。确保 公钥没有被改动。 之后 客户端生成一个随机数作为对称加密的 key 加密需要传送的数据 之后对key 使用证书的公钥加密  然后 hash  

服务器 使用私钥 解密 key 然后使用key 解密 数据。 
* 在浏览器中输入url地址 ->> 显示主页的过程（面试常客）

![](https://camo.githubusercontent.com/c7261a49ba596af8ab0029960a6507837279864e/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f342f31392f313632646235653938356161626462653f696d61676556696577322f302f772f313238302f682f3936302f666f726d61742f776562702f69676e6f72652d6572726f722f31)
DNS解析
TCP连接
发送HTTP请求
服务器处理请求并返回HTTP报文
浏览器解析渲染页面
连接结束
* 状态码

![](https://camo.githubusercontent.com/a508457c9a5252900e482a8ff8ff527970f8e9db/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f352f382f313633336531396462613237656430303f773d36373326683d32313826663d706e6726733d3732393638)

1. 200 成功
2. 301移动http-https 302+loaction重定向 304 缓存
3. 401 认证  403 授权 404 找不到 405 方法禁止 
4. 500 内部错误 502	Bad Gateway 504	Gateway Time-out
* http头信息
**请求**
    *  Accept：告诉WEB服务器自己接受什么介质类型，*/* 表示任何类型，type/* 表示该类型下的所有子类型，type/sub-type。
    * Content-Type： WEB 服务器告诉浏览器自己响应的对象的类型。例如：Content-Type：application/xml
    * Referer：发送请求页面URL。浏览器向 WEB 服务器表明自己是从哪个 网页/URL 获得/点击 当前请求中的网址/URL
    * Host： 发送请求页面所在域。
**响应**
    * refresh	应用于重定向或一个新的资源被创造，在5秒之后重定向（由网景提出，被大部分浏览器支持）Refresh: 5; url=http://www.zcmhi.com/archives/94.html
    * Allow	对某网络资源的有效的请求行为，不允许则返回405 Allow: GET, HEAD
* 禁用缓存

```java
response.setDateHeader("Expires", 0);
response.setHeader("Cache-Control", "no-cache");
response.setHeader("Pragma", "no-cache");
```
* **文件下载**

```java
// 配置文件下载
response.setHeader("content-type", "application/octet-stream");
response.setContentType("application/octet-stream");
// 下载文件能正常显示中文
response.setHeader("Content-Disposition", "attachment;filename=" + URLEncoder.encode(fileName, "UTF-8"));

```
* http 长连接
 
Connection：请求：close（告诉WEB服务器或者代理服务器，在完成本次请求的响应后，断开连接，不要等待本次连接的后续请求了）。
 keepalive（告诉WEB服务器或者代理服务器，在完成本次请求的响应后，保持连接，等待本次连接的后续请求）。 
 响应：close（连接已经关闭）。 
 keepalive（连接保持着，在等待本次连接的后续请求）。
Keep-Alive：如果浏览器请求保持连接，则该头部表明希望 WEB 服务器保持连接多长时间（秒）。例如：Keep-Alive：300

而从HTTP/1.1起，默认使用长连接，用以保持连接特性。使用长连接的HTTP协议，会在响应头加入这行代码：
`Connection:keep-alive`

服务端 keepalvie timeout

Keep-Alive模式，客户端如何**判断请求所得到的响应数据已经接收完成**：
1.Conent-Length
2.Transfer-Encoding: chunked
 Chunked编码将使用若干个Chunk串连而成，由一个标明长度为0的chunk标示结束

http协议很重要 。 在java 代码的协议配置 调优 都需要http协议的知识来支撑
keepalive 我需要过 两个这个相关的问题。
 1. NoHttpResponseException 这个是在生产环境 偶发的 我是用的resttemplate 底层也是httpclient。 也是配置的了
 tryhandler。 排查发现  是走不到 重试逻辑 。 （深层次的原因还是 keepalive  连接池为了性能考虑复用了连接。 但是连接已经被服务端关闭了）第一种方法 是 改写重试逻辑  第二种  连接存活时间改小 ，
 2. 做爬虫。 批量检查http服务是否可用   因为keepalive的原因 。导致连接一直未能关闭。 解决方法 改写 response处理逻辑。不去读流 直接关闭

其实“池”技术是一种通用的设计，其设计思想并不复杂：
1. 当有连接第一次使用的时候建立连接
2. 结束时对应连接不关闭，归还到池中
3. 下次同个目的的连接可从池中获取一个可用连接
4. 定期清理过期连接

# 安全方面

* sql注入
* XSS Cross-Site Scripting
* CSRF 跨站请求伪造( Cross-Site Request Forgery )
    csrf 有另lj于 xss，从政击效果上 ， 两者有重合的地方。从技术原理上两者有 本质的不同 ， xss 是在正常用户请求的 HTML 页面中执行了黑客提供的恶意代码， csrf 是黑客直接盗用用户浏览器中的登录信息 ， 冒充用户去执行黑客指定的操作。 xss 问题出在用户数据没有过滤 、 转义 l cs盯 问题出在 HTTP 接口没有防范不受信 任的调用。很多工程师会混淆这两个概念，甚至认为这两个卫生击是一样的。





# 分布式系统

## Spring Cloud
Spring Cloud 是规范 实现 有  Spring Cloud NetFlix and Spring Cloud Alibaba
![WX20190315-164937@2x](https://i.imgur.com/XQxLikC.png)
![1123](https://i.imgur.com/G2MpfMe.png)
### 注册中心  服务注册和发现

Nacos Discovery、Spring Cloud Netflix Eureka、ZooKeeper 和 Consul （原生）

### 服务消费者
rest （restTemplate）+ribbon 负载均衡 feign
### 配置中心 
Nacos Config 和 Spring Cloud Config  Apollo
### 断路器
Hystrix  Sentinel
### 网关
服务网关是微服务架构中一个不可或缺的部分。通过服务网关统一向外系统提供REST API的过程中，除了具备服务路由、均衡负载功能之外，它还具备了权限控制等功能
Zuul  Spring Cloud GateWay（原生）

## 分布式锁
## ID生成器
## 读写分离 分库分表
## 分布式事务

例如做一个服务，最初底下只有一个数据库，用数据库本身的事务来保证数据一致性。随着数据量增长到一定规模，进行了分库，这时数据库的事务就不管用了，如何保证多个库之间的数据一致性呢？

?> **7种解决方案**

### 2PC
2PC有两个角色：事务协调者和事务参与者。具体到数据库的实现来说，每一个数据库就是一个参与者，调用方也就是协调者。2PC是指事务的提交分为两个阶段，如图10-1所示。
* 阶段1：准备阶段。协调者向各个参与者发起询问，说要执行一个事务，各参与者可能回复YES、NO或超时。
* 阶段2：提交阶段。如果所有参与者都回复的是YES，则事务协调者向所有参与者发起事务提交操作，即Commit操作，所有参与者各自执行事务，然后发送ACK。

如果有一个参与者回复的是NO，或者超时了，则事务协调者向所有参与者发起事务回滚操作，所有参与者各自回滚事务，然后发送ACK，如图10-2所示。

![WX20190401-170113@2x](https://i.loli.net/2019/04/01/5ca1d3b567cfe.png ':size=300')

!> 2PC除本身的算法局限外，还有一个使用上的限制，就是它主要用在两个数据库之间（数据库实现了XA协议）。但以支付宝的转账为例，是两个系统之间的转账，而不是底层两个数据库之间直接交互，所以没有办法使用2PC。

### 最终一致性(消息中间件)

!> 实现了消息在发送方的不丢失、在接收方的不重复，联合起来就是消息的不漏不重，严格实现了系统A和系统B的最终一致性。
* 业务方直接实现 +kafaka
![WX20190401-171326@2x](https://i.loli.net/2019/04/01/5ca1d64de14cb.png)
* 基于RocketMQ事务消息
![WX20190401-173451@2x](https://i.loli.net/2019/04/01/5ca1db48c729f.png)
* 人工介入

### TCC
为了解决SOA系统中的分布式事务问题，支付宝提出了TCC。TCC是Try、Confirm、Cancel三个单词的缩写，其实是一个应用层面的2PC协议，Confirm对应2PC中的事务提交操作，Cancel对应2PC中的事务回滚操作，如图10-6所示。

*（1）准备阶段：调用方调用所有服务方提供的Try接口，该阶段各调用方做资源检查和资源锁定，为接下来的阶段2做准备。

*（2）提交阶段：如果所有服务方都返回YES，则进入提交阶段，调用方调用各服务方的Confirm接口，各服务方进行事务提交。如果有一个服务方在阶段1返回NO或者超时了，则调用方调用各服务方的Cancel接口，如图10-7所示。

![WX20190401-173639@2x](https://i.loli.net/2019/04/01/5ca1dbb7840ba.png)
### 事务状态表+调用方重试+接收方幂等

### 对账
### 妥协方案：弱一致性+基于状态的补偿
### 重试+回滚+报警+人工修复

## 分布式日志系统
### 概述

ELK 已经成为目前最流行的集中式日志解决方案，它主要是由Beats、Logstash、Elasticsearch、Kibana等组件组成，来共同完成实时日志的收集，存储，展示等一站式的解决方案。本文将会介绍ELK常见的架构以及相关问题解决。

`Filebeat`：Filebeat是一款轻量级，占用服务资源非常少的数据收集引擎，它是ELK家族的新成员，可以代替Logstash作为在应用服务器端的日志收集引擎，支持将收集到的数据输出到Kafka，Redis等队列。        
`Logstash`：数据收集引擎，相较于Filebeat比较重量级，但它集成了大量的插件，支持丰富的数据源收集，对收集的数据可以过滤，分析，格式化日志格式。         
`Elasticsearch`：分布式数据搜索引擎，基于Apache Lucene实现，可集群，提供数据的集中式存储，分析，以及强大的数据搜索和聚合功能。
`Kibana`：数据的可视化平台，通过该web平台可以实时的查看 Elasticsearch 中的相关数据，并提供了丰富的图表统计功能。

### 常见架构

* Logstash作为日志收集器

Logstash比较耗服务器资源，所以会增加应用服务器端的负载压力。

* **Filebeat作为日志收集器**

Filebeat作为应用服务器端的日志收集器(占用资源少)，一般Filebeat会配合Logstash一起使用，这种部署方式也是目前最常用的架构。

* 引入缓存队列的部署架构

这种架构主要是解决大数据量下的日志收集方案，使用缓存队列主要是解决数据安全与均衡Logstash与Elasticsearch负载压力。
![](https://static.oschina.net/uploads/space/2017/1130/131558_J7sa_2842105.png)
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
 * `Master`
 最稳定的分支
* `Develop`

主开发分支

 `Feature` 
 
 开发的时候切一个feature分支 开发完成后 合回本地的develop **(不要推送到远程Develop 因为代码未经过测试)**

 `Release` 
    * 测试分支 , 基于feature分支合并本地develop之后  , 从develop分支克隆 然后推送 此Release到远程
    * 主要用于提交给测试人员进行功能测试 , 测试过程中发现的BUG在本分支进行修复 , 修复完成上线后合并到develop/master分支并推送(完成功能) , 打Tag
    * 属于临时分支 , 功能上线后可选删除
`HotFix` 

![](https://img-blog.csdn.net/20180803135443287?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpbmdiYW96aGVuMTIxMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
# 补充

## 限流 熔断
## RPC
# 消息队列

# Apollo  哨兵  elstic job  motan dubbo elk docker es  hbase jenkins git nginx  

# 亮点 openApi 模板化 自定义注释 统一 gateway入口   适配

# zigbee 终端节点 汇聚节点 自组网  低功耗 通信协议 蓝牙 wifi
