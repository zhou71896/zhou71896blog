---
title: java常用面试题
date: 2018-03-16 13:25:14
tags: java
---

## 1.什么是可变参数?
  在 Java 5 中提供了变长参数，允许在调用方法时传入不定长度的参数。
  变长参数是Java的一个语法糖，本质上还是基于数组的实现:
{% codeblock lang:bash %}
void foo(String... args);
void foo(String[] args);
{% endcodeblock %}
## 2.断言的用途?
断言是在Java1.4中引入的。它能让验证假设。如果断言失败（即返回false），就会抛出AssertionError（如果启用断言）。
## 3.什么时候使用断言?
　1.编写代码时，总是会做出一些假设，断言就是用于在代码中捕捉这些假设。断言表示为一些布尔表达式，程序员相信在程序中的某个特定点该表达式值为真，可以在任何时候启用和禁用断言验证，因此可以在测试时启用断言而在部署时禁用断言。同样，程序投入运行后，最终用户在遇到问题时可以重新启用断言。
　2.使用断言可以创建更稳定、品质更好且 不易于出错的代码。当需要在一个值为FALSE时中断当前操作的话，可以使用断言。单元测试必须使用断言（Junit/JunitX）。
　3.除了类型检查和单元测试外，断言还提供了一种确定各种特性是否在程序中得到维护的极好的方法
## 4.什么是垃圾回收?
  垃圾收集GC（Garbage Collection）是Java语言的核心技术之一，之前我们曾专门探讨过Java 7新增的垃圾回收器G1的新特性，但在JVM的内部运行机制上看，Java的垃圾回收原理与机制并未改变。垃圾收集的目的在于清除不再使用的对象。
GC通过确定对象是否被活动对象引用来确定是否收集该对象。
## 5.用一个例子解释垃圾回收?
比如你运行一个程序,是不是要先把程序代码放到内存里执行?
执行完了,这段代码就会一直存在内存中,占用了内存的使用空间,如果是C语言的话,是要程序员在设计程序的时候用一个垃圾回收的指令把这段程序代码从内存中清理掉,但是java的话,程序员是不用再编写一个清理程序代码垃圾回收的语句的,而是由java的虚拟机垃圾回收机制自动执行,就是说,每隔一段时间java虚拟机会自动检测内存中是否存在没用的程序代码在占用内存,如果是的话就会把这些没用的或者使用过的内存中的代码清理掉,一般是说回收了垃圾所以说java程序有时候会觉得比较占内存的原因也是这个,不过因为java虚拟机有这个回收垃圾的机制,方便了程序员编写代码。
## 6.什么时候运行垃圾回收?
垃圾收集器跟踪每一个对象，收集那些不可触及的对象（即该对象不再被程序引用 了），回收其占有的内存空间。但在进行垃圾收集的时候，垃圾收集器会调用该对象的finalize(   )方法（如果有）。如果在finalize()方法中，又使得该对象被程序引用(俗称复活了)，则该对象就变成了可触及的对象，暂时不会被垃圾收集了。但是由于每个对象只能调用一次finalize(   )方法，所以每个对象也只可能 "复活 "一次。
## 7.垃圾回收的最佳做法?
用编程的方式，我们可以要求(记住这只是一个请求——不是一个命令)JVM通过调用System.gc()方法来运行垃圾回收。
当内存已满，且堆上没有对象可用于垃圾回收时，JVM可能会抛出OutOfMemoryException。
对象在被垃圾回收从堆上删除之前，会运行finalize()方法。我们建议不要用finalize()方法写任何代码。
## 8.什么是初始化数据块?
初始化数据块——当创建对象或加载类时运行的代码。
有两种类型的初始化数据块：
1、静态初始化器：加载类时运行的的代码；
2、实例初始化器：创建新对象时运行的代码。
## 9.什么是静态初始化器？
　　静态初始化器是由关键字static引导的一对大括号括起的语句组。它的作用与类的构造函数有些相似，都用来完成初始化的工作，但是静态初始化器与构造函数有三点根本的不同：
　　（1）构造函数是对每个新创建的对象初始化，而静态初始化器是对每个类进行初始化；
　　（2）构造函数是在用new运算符产生新对象时由系统自动执行，而静态初始化器则是在它所属的类加载入内存时由系统调用运行的；
　　（3）不同于构造函数，静态初始化器不是方法，没有方法名、返回值和参数列表。
## 10.什么是实例初始化块？
实例初始化就是在内存中开辟一个类的对象  如：
{% codeblock lang:java %}
public class Animal{
  public Animal(){ }
  public void mthod(){  }
}
{% endcodeblock %}
在main函数中通过语句 Animal a = new Animal();
表示把类Animal实例化，a为其对象引用
## 11.什么是正则表达式?
正则表达式，又称规则表达式。（英语：Regular Expression，在代码中常简写为regex、regexp或RE），计算机科学的一个概念。正则表达式通常被用来检索、替换那些符合某个模式(规则)的文本。
## 12.什么是令牌化？
令牌化是指在分隔符的基础上将一个字符串分割为若干个子字符串。
## 13.给出令牌化的例子?
例如，分隔符；分割字符串ac;bd;def;e为四个子字符串ac，bd，def和e。
分隔符自身也可以是一个常见正则表达式。
String.split(regex)函数将regex作为参数。
## 14.如何使用扫描器类(Scanner Class)令牌化?
{% codeblock lang:java %}
private static void tokenizeUsingScanner(String string,String regex) {
    Scanner scanner = new Scanner(string);
    scanner.useDelimiter(regex);
    List<String> matches = new ArrayList<String>();
    while(scanner.hasNext()){
        matches.add(scanner.next());
    }
    System.out.println(matches);
}
tokenizeUsingScanner("ac;bd;def;e",";");//[ac, bd, def, e]
{% endcodeblock %}
## 15.如何添加小时(hour)到一个日期对象(Date Objects)?
{% codeblock lang:java %}
Date date = new Date();
//Increase time by 6 hrs
date.setTime(date.getTime() + 6 * 60 * 60 * 1000);
System.out.println(date);
//Decrease time by 6 hrs
date = new Date();
date.setTime(date.getTime() - 6 * 60 * 60 * 1000);
System.out.println(date);
{% endcodeblock %}
## 16.如何格式化日期对象?
格式化日期需要使用DateFormat类完成。让我们看几个例子。
{% codeblock lang:java %}
System.out.println(DateFormat.getDateInstance(
        DateFormat.FULL, new Locale("it", "IT"))
        .format(date));//marted“ 16 ottobre 2012
System.out.println(DateFormat.getDateInstance(
        DateFormat.FULL, Locale.ITALIAN)
        .format(date));//marted“ 16 ottobre 2012
//This uses default locale US
System.out.println(DateFormat.getDateInstance(
        DateFormat.FULL).format(date));//Tuesday, October 16, 2012
System.out.println(DateFormat.getDateInstance()
        .format(date));//Oct 16, 2012
System.out.println(DateFormat.getDateInstance(
        DateFormat.SHORT).format(date));//10/16/12
System.out.println(DateFormat.getDateInstance(
        DateFormat.MEDIUM).format(date));//Oct 16, 2012
System.out.println(DateFormat.getDateInstance(
        DateFormat.LONG).format(date));//October 16, 2012
{% endcodeblock %}
## 17.java中日历类(Calendar Class)的用途?
Calendar类在Java中用于处理日期。Calendar类提供了增加和减少天数、月数和年数的简便方法。它还提供了很多与日期有关的细节（这一年的哪一天？哪一周？等等）
## 18.如何在Java中获取日历类的实例?
Calendar类不能通过使用new Calendar创建。得到Calendar类实例的最好办法是在Calendar中使用getInstance() static方法。
## 19.解释一些日历类中的重要方法?
在Calendar对象上设置日（day），月（month）或年（year）不难。对Day，Month或Year调用恰当Constant的set方法。下一个参数就是值。
{% codeblock lang:java %}
calendar.set(Calendar.DATE, 24);
calendar.set(Calendar.MONTH, 8);//8 - September
calendar.set(Calendar.YEAR, 2010);
System.out.println(calendar.get(Calendar.YEAR));//2010
System.out.println(calendar.get(Calendar.MONTH));//8
System.out.println(calendar.get(Calendar.DATE));//24
System.out.println(calendar.get(Calendar.WEEK_OF_MONTH));//4
System.out.println(calendar.get(Calendar.WEEK_OF_YEAR));//39
System.out.println(calendar.get(Calendar.DAY_OF_YEAR));//267
System.out.println(calendar.getFirstDayOfWeek());//1 -> Calendar.SUNDAY
{% endcodeblock %}
## 20.数字格式化类(Number Format Class)的用途?
{% codeblock lang:java %}
//数字格式用于格式化数字到不同的区域和不同格式中。
//使用默认语言环境的数字格式
System.out.println(NumberFormat.getInstance().format(321.24f));//321.24
//使用区域设置的数字格式
//使用荷兰语言环境格式化数字：
System.out.println(NumberFormat.getInstance(new Locale("nl")).format(4032.3f));//4.032,3
//使用德国语言环境格式化数字：
System.out.println(NumberFormat.getInstance(Locale.GERMANY).format(4032.3f));//4.032,3
//使用默认语言环境格式化货币
System.out.println(NumberFormat.getCurrencyInstance().format(40324.31f));//$40,324.31
//使用区域设置格式化货币
//使用荷兰语言环境格式化货币：
System.out.println(NumberFormat.getCurrencyInstance(new Locale("nl")).format(40324.31f));//? 40.324,31
{% endcodeblock %}
## 21.Spring 事务的隔离性，说说每个隔离性的区别
Isolation Level(事务隔离等级):
1、Serializable：最严格的级别，事务串行执行，资源消耗最大；
2、REPEATABLE READ：保证了一个事务不会修改已经由另一个事务读取但未提交（回滚）的数据。避免了“脏读取”和“不可重复读取”的情况，但是带来了更多的性能损失。
3、READ COMMITTED:大多数主流数据库的默认事务等级，保证了一个事务不会读到另一个并行事务已修改但未提交的数据，避免了“脏读取”。该级别适用于大多数系统。
4、Read Uncommitted：保证了读取过程中不会读取到非法数据。
## 22.Spring 事务的传播行为，说说每个传播行为的区别
Propagation 
PROPAGATION_REQUIRED--支持当前事务，如果当前没有事务，就新建一个事务。这是最常见的选择。 
PROPAGATION_SUPPORTS--支持当前事务，如果当前没有事务，就以非事务方式执行。 
PROPAGATION_MANDATORY--支持当前事务，如果当前没有事务，就抛出异常。 
PROPAGATION_REQUIRES_NEW--新建事务，如果当前存在事务，把当前事务挂起。 
PROPAGATION_NOT_SUPPORTED--以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。 
PROPAGATION_NEVER--以非事务方式执行，如果当前存在事务，则抛出异常。
## 23.hibernate跟Mybatis/ibatis的区别,为什么选择使用它?
hibernate的真正掌握（封装的功能和特性非常多）要比Mybatis来得难。
在真正产品级应用上要用Hibernate，不仅对开发人员的要求高，hibernate往往还不适合（多表关联查询等）。
Hibernate:
 * 制定合理的缓存策略；
 * 尽量使用延迟加载特性；
 * 采用合理的Session管理机制；
 * 使用批量抓取，设定合理的批处理参数（batch_size）
 * 进行合理的O/R映射设计
Mybatis：
 * MyBatis在Session方面和Hibernate的Session生命周期是一致的，同样需要合理的Session管理机制。MyBatis同样具有二级缓存机制。 
 * MyBatis可以进行详细的SQL优化设计
	SQL优化方面
Hibernate的查询会将表中的所有字段查询出来，这一点会有性能消耗。
Hibernate也可以自己写SQL来指定需要查询的字段，但这样就破坏了Hibernate开发的简洁性。
Mybatis的SQL是手动编写的，所以可以按需求指定查询的字段。
总的来说，Hibernate使用的是封装好，通用的SQL来应付所有场景，而Mybatis是针对响应的场景设计的SQL。Mybatis的SQL会更灵活、可控性更好、更优化。
实际项目关于Hibernate和Mybatis的选型：
	移植性
Hibernate与具体数据库的关联只需在XML文件中配置即可，所有的HQL语句与具体使用的数据库无关，移植性很好。
MyBatis项目中所有的SQL语句都是依赖所用的数据库的，所以不同数据库类型的支持不好。
	JDBC
Hibernate是在JDBC上进行了一次封装。
Mybatis是基于原生的JDBC的。Mybatis有运行速度上的优势。
	功能、特性丰富程度
Hibernate提供了诸多功能和特性。要全掌握很难。
Mybatis 自身功能很有限，但Mybatis支持plugin，可以使用开源的plugin来扩展功能。
	动态SQL
Mybatis mapper xml 支持动态SQL
Hibernate不支持
1、数据量：有以下情况最好选用Mybatis
如果有超过千万级别的表
如果有单次业务大批量数据提交的需求（百万条及以上的），这个尤其不建议用Hibernate
如果有单次业务大批量读取需求（百万条及以上的）(注，hibernate多表查询比较费劲，用不好很容易造成性能问题)
2、表关联复杂度
如果主要业务表的关联表超过20个（大概值），不建议使用hibernate
3、人员
如果开发成员多数不是多年使用hibernate的情况，建议使用mybatis
4、数据库对于项目的重要程度
如果项目要求对于数据库可控性好，可深度调优，用mybatis

## 24.structs跟Spring mvc的优缺点，让你选会如何选择?
1、spring3开发效率高于struts；
2、spring3 mvc可以认为已经100%零配置；
3、struts2是类级别的拦截， 一个类对应一个request上下文，springmvc是方法级别的拦截，一个方法对应一个request上下文，而方法同时又跟一个url对应。所以说从架构本身上 spring3 mvc就容易实现restful url，而struts2的架构实现起来要费劲。因为struts2 action的一个方法可以对应一个url，而其类属性却被所有方法共享，这也就无法用注解或其他方式标识其所属方法了；
4、spring3mvc的方法之间基本上独立的，独享request response数据，请求数据通过参数获取，处理结果通过ModelMap交回给框架，方法之间不共享变量。而struts2搞的就比较乱，虽然方法之间也是独立的，但其所有Action变量是共享的。这不会影响程序运行，却给编码读程序时带来麻烦 ；
5、由于Struts2需要针对每个Request进行封装，把Request，Session等Servlet生命周期的变量封装成一个一个Map，供给每个Action使用，并保证线程安全。所以在原则上，是比较耗费内存的

## 25.简单说说Spring事务机制
Spring事务管理主要包括3个接口，Spring的事务主要是由他们三个共同完成的。
1.PlatformTransactionManager：事务管理器--主要用于平台相关事务的管理
 主要有三个方法：
	  commit  事务提交；
      rollback  事务回滚；
      getTransaction  获取事务状态。
2.TransactionDefinition：事务定义信息--用来定义事务相关的属性，给事务管理器PlatformTransactionManager使用
这个接口有下面四个主要方法：
getIsolationLevel：获取隔离级别；
getPropagationBehavior：获取传播行为；
getTimeout：获取超时时间；
isReadOnly：是否只读（保存、更新、删除时属性变为false--可读写，查询时为true--只读）
事务管理器能够根据这个返回值进行优化，这些事务的配置信息，都可以通过配置文件进行配置。
3.TransactionStatus：事务具体运行状态--事务管理过程中，每个时间点事务的状态信息。
例如它的几个方法：
hasSavepoint()：返回这个事务内部是否包含一个保存点，
isCompleted()：返回该事务是否已完成，也就是说，是否已经提交或回滚
isNewTransaction()：判断当前事务是否是一个新事务
声明式事务的优缺点：
优点
不需要在业务逻辑代码中编写事务相关代码，只需要在配置文件配置或使用注解（@Transaction），这种方式没有侵入性。
缺点
声明式事务的最细粒度作用于方法上，如果像代码块也有事务需求，只能变通下，将代码块变为方法。
## 26.Spring 4.0新特性
pring4新特性——泛型限定式依赖注入
Spring4新特性——核心容器的其他改进
Spring4新特性——Web开发的增强
Spring4新特性——集成Bean Validation 1.1(JSR-349)到SpringMVC 
Spring4新特性——Groovy Bean定义DSL
Spring4新特性——更好的Java泛型操作API 
Spring4新特性——JSR310日期API的支持
Spring4新特性——注解、脚本、任务、MVC等其他特性改进 
## 27.weblogic 负载均衡的原理和集群的配置
Weblogic支持集群技术，即让一组Server指向同一域名一起工作从而提供一个更强大、更可靠的应用平台。对于客户端而言，无论Cluster中有几个Server在工作，看上去都是一个。集群技术有两个最明显的特色：
(1)可伸缩性：Cluster对加入其中的Server在性能上没有限制，为了提高性能，当客户端的请求大幅增加时，可以动态地向Cluster中添加Server。并且，配置Cluster当一台机器的资源没有被完全利用时，可以在同一机器上启动多个Server，但要求每一个Server使用不同的IP，而不能用同一IP的不同端口。
(2)高可用性：由于在Cluster中同一service在多个Server上同时存放或放在一个共享文件系统中，因此相同的请求可以有多个Server提供，并且Server间还可以复制状态信息。这样，当其中某一Server宕机或无法响应请求时，其它的Server会立即接管它的任务，从而把应用和客户端完全隔离开来。
{% blockquote @传送门 http://blog.csdn.net/zdwzzu2006/article/details/6528641 %}
{% endblockquote %}
## 28.Nginx+Tomcat+Redis 实现负载均衡，资源分离，session共享
{% blockquote @传送门 http://blog.csdn.net/u014756827/article/details/51545766 %}
{% endblockquote %}
## 29.nginx配置文件详解---nginx.conf
{% blockquote @传送门 http://blog.csdn.net/tjcyjd/article/details/50695922 %}
{% endblockquote %}
## 30.web如何项目优化
{% blockquote @传送门 https://bbs.csdn.net/topics/391849317 %}
{% endblockquote %}
## 31.单例模式有几种？如何优化?
{% blockquote @传送门 https://www.cnblogs.com/Ycheng/p/7169381.html %}
{% endblockquote %}
## 32.简单说说线程池的原理和实现
{% blockquote @传送门 http://blog.csdn.net/he90227/article/details/52576452 %}
{% endblockquote %}
## 33.项目并发如何处理?(web项目)
{% blockquote @传送门 https://www.cnblogs.com/lr393993507/p/5909804.html %}
{% endblockquote %}
## 34.简单说说功能权限存在的水平权限漏洞和垂直权限漏洞的场景和解决办法(目前权限界别就是功能权限)
{% blockquote @传送门 http://www.bubuko.com/infodetail-196677.html %}
{% endblockquote %}
## 35.平台上的图片如何防盗链
{% blockquote @传送门 http://blog.csdn.net/likaibk/article/details/52879514 %}
{% endblockquote %}
## 36.如何区分上传的图片是不是木马?
{% blockquote @传送门 http://blog.csdn.net/lenny_cl/article/details/55045866 %}
{% endblockquote %}
## 37.消息队列的原理和实现
{% blockquote @传送门 http://blog.csdn.net/lzq_csdn_th/article/details/51945408 %}
{% endblockquote %}
## 38.mysql查询字段区不区分大小写?区不区分大小的应用含义有哪些?
{% blockquote @传送门 http://www.jb51.net/article/70884.htm %}
{% endblockquote %}
## 39.简单说说数据库集群和负载均衡，分布式
{% blockquote @传送门 https://www.zhihu.com/question/20695647 %}
{% endblockquote %}
## 40存储过程的结构和优点
{% blockquote @传送门 https://www.cnblogs.com/ego/archive/2012/12/06/2804592.html %}
{% endblockquote %}
## 41触发器的原理和作用
{% blockquote @传送门 https://www.cnblogs.com/l1pe1/p/7910395.html %}
{% endblockquote %}






