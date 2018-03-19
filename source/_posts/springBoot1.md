---
title: SpringBoot(一)
date: 2018-03-19 13:44:10
tags: SpringBoot
categories: Spring
---
# SpringBoot的简介

对构建生产就绪的Spring应用程序提出自己的观点。Spring Boot支持约定而非配置，旨在让您尽快启动并运行。

Spring Boot可以轻松创建独立的，生产级的基于Spring的应用程序，您可以“运行”。我们对Spring平台和第三方库采用了独特的技术视角，所以您可以花很小的代价就可以开始。大多数Spring Boot应用程序只需要很少的Spring配置。

# 特征
 * 创建独立的Spring应用程序 
 * 直接嵌入Tomcat，Jetty或Undertow（无需部署WAR文件）
 * 提供自己的'入门'POM来简化你的Maven配置
 * 尽可能自动配置Spring
 * 提供生产就绪功能，如指标，运行状况检查和外部配置
 * 绝对不会生成代码，并且不需要XML配置

# 快速开始
在Maven的配置当中添加相关的配置如下:
{% codeblock lang:java %}
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.0.RELEASE</version>
</parent>
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
{% endcodeblock %}

helllo/SampleController.java
{% codeblock lang:java %}
package hello;

import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.stereotype.*;
import org.springframework.web.bind.annotation.*;

@Controller
@EnableAutoConfiguration
public class SampleController {

    @RequestMapping("/")
    @ResponseBody
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(SampleController.class, args);
    }
}
{% endcodeblock %}

# 用SpringBoot来构建Restful Web Service相关应用

接下来我们将来构建一个Restful Web Service的应用

# 目的
构建的服务将会以http get请求: 
{% codeblock lang:java %}
http://localhost:8080/greeting 
{% endcodeblock %}
同时将会得到一个Json返回值
{% codeblock lang:java %}
{"id":1,"content":"Hello, World!"}
{% endcodeblock %}
如果通过自定义传参数的方式访问查询的:
{% codeblock lang:java %}
http://localhost:8080/greeting?name=User 
{% endcodeblock %}
当前的参数将会被返回回来:
{% codeblock lang:java %}
{"id":1,"content":"Hello, User!"}
{% endcodeblock %}

# 我们需要怎么操作呢?
 * 大概15分钟
 * 一个你喜欢的IDE
 * JDK1.8+
 * Gradle 2.3+ 或者Maven 3.0+
 * 你也可以把相关的代码直接导入到你的IDE IntelliJ IDEA
# 我们就来完成这个操作吧
 这里我们使用Maven来构建当前的项目
 在我们的项目当中我们的文件目录是这样的: src/main/java/hello
 接下来是pom.xml文件
 {% codeblock lang:java %}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.springframework</groupId>
    <artifactId>gs-rest-service</artifactId>
    <version>0.1.0</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.0.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.jayway.jsonpath</groupId>
            <artifactId>json-path</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <properties>
        <java.version>1.8</java.version>
    </properties>


    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

    <repositories>
        <repository>
            <id>spring-releases</id>
            <url>https://repo.spring.io/libs-release</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-releases</id>
            <url>https://repo.spring.io/libs-release</url>
        </pluginRepository>
    </pluginRepositories>
</project>
{% endcodeblock %}
 然后我们配置好了我们需要pom文件之后。
 接下来在当前的项目当中我们要开始创建相关的资源呈现类,刚才我们的服务将会以Get的方式/greeting请求到,
 然后在请求成功的基础(200)上.返回一个固定的JSON格式就像下面这样的:
{% codeblock lang:java %}
{"id":1,"content":"Hello, World!"}
{% endcodeblock %}
id这个字段应该是一个唯一标示在当前的对话请求中,内容则是当前对话中的一个文本显示。
那么我们为了构建一个打招呼内容的呈现，我们就需要创建一个资源呈现的类。并且我们会提供一个老式的带属性的
java对象,并且会有相关的构造器和相关对id和content对应的访问权限。
相关的类位置:
src/main/java/hello/Greeting.java
{% codeblock lang:java %}
package hello;

public class Greeting {

    private final long id;
    private final String content;

    public Greeting(long id, String content) {
        this.id = id;
        this.content = content;
    }

    public long getId() {
        return id;
    }

    public String getContent() {
        return content;
    }
}
{% endcodeblock %}
接下来我们将创建资源控制器来为这些招呼会话们提供服务

# 创建资源控制器
在Spring 项目中构造RESTFUL web services,HTTP  requests 会被控制器Controller来进行处理。并且这些组件能够以`@RestController`注解
方式轻易的被识别到,并且GreetingController 在处理/greeting的GET请求,将会以返回一个新的Greeting class实例来回应。
相关的类位置:
src/main/java/hello/GreetingController.java
{% codeblock lang:java %}
package hello;

import java.util.concurrent.atomic.AtomicLong;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @RequestMapping("/greeting")
    public Greeting greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return new Greeting(counter.incrementAndGet(),
                            String.format(template, name));
    }
}
{% endcodeblock %}
看吧，这个控制器的类还是比较精简，但是这对我们要完成的业务来说已经足够啦，那我们就一步一步的完成它吧。
我们接下来将会使用@RequestMapping 注解来保证HTTP请求 /greeting 能够映射到当前greeting()方法当中。
当然这里需要特别强调的是:我们并没有指定当前方法的具体请求方式(GET,POST,PUT)等等这些啦，这里是因为我们@RequestMapping 映射所有的HTTP操作的时候已默认的@RequestMapping(method=GET)来限定当前的映射。
用@RequestParam注解 来绑定我们当前请求的字符串参数name,并且把当前的参数传进我们的gretting()方法当中。
这个查询的字符参数将会被自动标示为(required=true 默认): 如果没有当前参数的话，那么默认的"World"将会被使用。
然后我们可以看到方法体当中，创建并且返回了一个基于counter计数器自动计数的id和content属性Greeting的对象,并通过使用greeting的模板来格式话对应所给的名称。
传统mvc的控制器和restful web service控制器最大的不同是在Http response响应体的创建方式上。
不同于依赖于视图技术呈现服务端的渲染greeting数据成为HTML,我们的这个RESTFUL web 服务控制器简单输出并返回Greeting 对象,而且这个对象数据将会被直接以JSON的形式写到Httpresponse当中。
这段代码当中使用的是Spring4的@RestController注解,这个注解主要作用是将当前类，标记为一个值返回为对象而不是视图的控制器,它兼顾了@Controller和@ResponseBody。
Greeting对象会被转化成为JSON,你不需要手动来转换,得益于Spring`s HTTP 信息转换支持,因为Jackson2会在Classpath中帮转,通过Spring·s MappingJackson2HttpMessageConverter类将会自动将Greeting instance对象转换为JSON。

# 使当前的应用程序可执行
尽管可以把当前发服务打包成为传统的war包来部署到外部的应用服务器上,更简洁的方法是单独创建一个独立的应用。
你可以把所有的内容打成一个可以执行jar文件,由以前的java main()方法驱动执行。
并且你可以使用Spring支持的方式在http runtime 的时候内嵌入Tomcat Servlet container,而不是单独推送一个额外的实体对象。
相关的类位置:
src/main/java/hello/Application.java
{% codeblock lang:java %}
package hello;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
	
        SpringApplication.run(Application.class, args);
    }
}
{% endcodeblock %}
@SpringBootApplication 注解会很方便的添加如下的一些功能:
 * @Configuration 标示当前类作为应用程序的上下文对象bean定义的来源
 * @EnableAutoConfiguration 告诉SpringBoot在启动的时候基于classPath来添加对应的beans，其他的beans和丰富的特性配置
 * 正常情况下你需要在Spring MVC 应用中添加@EnableWebMvc,但是在SpringBoot当中这部分功能将会被自动添加,你可以在classPath当中的Spring-webmvc看到。
这个标志着作为web应用主要的行为都能够被激活，比如像构建DisptatcherSerlet(分发Servlet)。
 * @ComponentScan 告诉Spring 去寻找其他的对象和配置以及相关的服务，在hello package当中，并且允许它去发现controllers(其他控制器)。
 
# 构建一个可执行的JAR文件
你可以在Gradle 或者 Maven 当中通过命令行的方式运行你的应用程序。
或者你可以大度打一个包含了必要依赖和classes以及资源的可执行的jar文件,并且运行它。
这样的话很容易封装，规划版本，并且能够不同的跨环境，在有限开发周期中部署服务到应用当中。
如果你使用的是Maven,你可可以运行applicaiton 使用 ./mvnw spring-boot run。或者你可以通过命令./mvnw clean package构建JAR文件。
并且你可以运行当前的jar文件:
java -jar target/gs-rest-service-0.1.0.jar
 
输出显示当前的，服务将会在几秒中之后上线并且运行。
 
# 测试当前的服务
现在你可以看到当前服务上线了，访问 http://localhost:8080/greeting,你会看到:
{% codeblock lang:java %} 
 {"id":1,"content":"Hello, World!"}
{% endcodeblock %}
提供一个name参数访问当前的地址http://localhost:8080/greeting?name=User。
注意content值的变化，从"Hello, World!"变成"Hello User!"
{% codeblock lang:java %} 
{"id":2,"content":"Hello, User!"}
{% endcodeblock %}
这个改变表明@RequestParam注解在GreetingController当中运行的很正常。name参数被给与了一个默认值"world"。
但是也可以被重写通过传入查询的参数。
同时你可以看到id的变化由1变到了2，这证明了你多次访问的是同一个GreetingController实体，并且它的计数器部分预期加1。
# 收尾
恭喜！我们已经成功的使用Spring开发了一个Restful web service。相关配置和注解确实让开发变得更为简洁干净。
 