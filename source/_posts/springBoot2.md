---
title: springBoot(二)
date: 2018-03-20 14:42:47
tags: SpringBoot
categories: Spring
---

# 访问mysql当中的数据

这个教程将会指导你如何创建一个连接mysql数据库的Spring应用,主要使用的SpringData JPA技术来连接数据库，但是这只是其中的选择之一(你也可以使用Spring JDBC)

# 要做什么呢?

你将会创建一个MySQL的数据库,创建一个Spring application 并且连接一个新建的数据库

# 需要什么呢?
 * mysql 5.6+.如果你有安装docker的话，可以试试作为装载器运行数据库
 * 大约15分钟
 * 你喜欢的IDE
 * JDK 1.8+
 * Gradle 2.3+ 或者 Maven 3.0+
 * 你也可以直接导入代码到你的IDE
 
# 完善每一步
 
用Maven来构建当前的项目
首先你要创建你的文件结构, 你可以创建 mkdir -p src/main/java/hello (在*nix系统上面)
以下是pom.xml文件的相关配置:
{% codeblock lang:java %}
 <?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.springframework</groupId>
    <artifactId>gs-mysql-data</artifactId>
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

        <!-- JPA Data (We are going to use Repositories, Entities, Hibernate, etc...) -->

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <!-- Use MySQL Connector-J -->

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
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
</project>
{% endcodeblock %}
我们可以看看Spring Boot Maven plugin提供了很多方便的特征:
 * 它手机了所有在classpath的jar,并且打包出单独可以执行的jar包，让执行和运输到你的服务上变的更加方便。
 * 它会搜索所有的public static void main() 方法把它标记为可执行的类。
 * 并且它提供了一个解决依赖版本的方案，你可以重新任何你想写的版本。
创建数据库
来到后台的终端，打开MySQL 客户端
比如说在windows下面的命令行:
{% codeblock lang:java %}
mysql -u root -p
{% endcodeblock %}
创建了一个新的数据库
{% codeblock lang:java %}
create database db_example; -- 创建一个新的数据库
create user 'springuser'@'localhost' identified by 'root'; -- 创建用户
grant all on db_example.* to 'springuser'@'localhost' -- 把所有的权限给这个新的用户
{% endcodeblock %}

创建一个application.properties文件
SpringBoot当中会默认给你一个默认的选择，默认的数据库是h2。因此当你想要改变并且使用其他的数据库的时候，你要在application.properties文件中定义相关的属性
具体的文件创建路径如下:
src/main/resources/application.properties
{% codeblock lang:java %}
spring.jpa.hibernate.ddl-auto=create
spring.datasource.url=jdbc:mysql://localhost:3306/db_example
spring.datasource.username=springuser
spring.datasource=springuser
spring.datasource.password=ThePassword
{% endcodeblock %}
此处,spring.jpa.hibernate.ddl-auto的值能够是none,update,create,create-drop
	* none 这个是mysql的默认配置，数据库的结构没有改变
	* update Hibernate 根据给出的实体结构改变了数据库
	* create 每次创建数据库，但是在关闭的时候不会丢弃它
	* create-drop 创建数据库，当SessionFactory关闭的时候丢弃它
此处我们使用的是create因为我们没有相关的数据库结构,再第一次运行了之后，我们在把当前的模式切换为update或者none根据程序的需要。在我们对当前的数据库的机构改变了之后我们改成update。
默认的数据库是H2并且它所选用的模式是create-drop。但对于其他像MySQL是none

# 创建@Entity model

src/main/java/hello/User.java
{% codeblock lang:java %}
package hello;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity // This tells Hibernate to make a table out of this class
public class User {
    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private Integer id;

    private String name;

    private String email;

	public Integer getId() {
		return id;
	}

	public void setId(Integer id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getEmail() {
		return email;
	}

	public void setEmail(String email) {
		this.email = email;
	}
}
{% endcodeblock %}
这个实体类将会通过Hibernate自动被翻译到表当中
# 创建repository
src/main/java/hello/UserRepository.java
{% codeblock lang:java %}
package hello;

import org.springframework.data.repository.CrudRepository;

import hello.User;

// This will be AUTO IMPLEMENTED by Spring into a Bean called userRepository
// CRUD refers Create, Read, Update, Delete

public interface UserRepository extends CrudRepository<User, Long> {

}
{% endcodeblock %}
这个接口,将会自动实现通过Spring相同名称的bean叫做userRepository

# 为你的Spring应用创建一个新的控制器
src/main/java/hello/MainController.java

{% codeblock lang:java %}
package hello;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

import hello.User;
import hello.UserRepository;

@Controller    // This means that this class is a Controller
@RequestMapping(path="/demo") // This means URL's start with /demo (after Application path)
public class MainController {
	@Autowired // This means to get the bean called userRepository
	           // Which is auto-generated by Spring, we will use it to handle the data
	private UserRepository userRepository;

	@GetMapping(path="/add") // Map ONLY GET Requests
	public @ResponseBody String addNewUser (@RequestParam String name
			, @RequestParam String email) {
		// @ResponseBody means the returned String is the response, not a view name
		// @RequestParam means it is a parameter from the GET or POST request

		User n = new User();
		n.setName(name);
		n.setEmail(email);
		userRepository.save(n);
		return "Saved";
	}

	@GetMapping(path="/all")
	public @ResponseBody Iterable<User> getAllUsers() {
		// This returns a JSON or XML with the users
		return userRepository.findAll();
	}
}
{% endcodeblock %}

# 执行当前的程序
通过Applicaiton嵌入到Tomcat servlet容器当中来发布。
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

# 测试当前的程序
在刚才的基础上我们来测试当前的应用
localhost:8080/demo/all 获取所有的数据 localhost:8080/demo/add 添加一个用户的数据
{% codeblock lang:java %}
$ curl 'localhost:8080/demo/add?name=First&email=someemail@someemailprovider.com'
{% endcodeblock %}
回应的结果应该是
{% codeblock lang:java %}
Saved
{% endcodeblock %}
{% codeblock lang:java %}
$ curl 'localhost:8080/demo/all'
{% endcodeblock %}
回应的结果应该是
{% codeblock lang:java %}
[{"id":1,"name":"First","email":"someemail@someemailprovider.com"}]
{% endcodeblock %}

# 改变一下安全配置
如果将当前的发布到正式环境，你也许会遭遇到SQL 注入的攻击，因此我们需要的SQL命令,作为安全起见的话，在我们发布之前我们需要收回相关的权限。
{% codeblock lang:java %}
mysql> revoke all on db_example.* from 'springuser'@'localhost';
{% endcodeblock %}
在收回了所有的关于当前用户的权限之后，我们需要我们的应用程序能够做一些事情，因此我们需要给它赋予以下权限:
{% codeblock lang:java %}
mysql> grant select, insert, delete, update on db_example.* to 'springuser'@'localhost';
{% endcodeblock %}
并且现在我们需要改变以下我们的配置文件 src/main/resources/application.properties
{% codeblock lang:java %}
spring.jpa.hibernate.ddl-auto=none
{% endcodeblock %}
只有在你第一磁需要根据你的实体在表中创建实体才需要吧状态改为 create
# 总结
恭喜！你已经开发了一个可以链接MySQL数据库的Spring application!
