---
title: SpringCloud配置
date: 2018-03-19 11:10:44
tags:
---

Spring Cloud Config为分布式系统中的外部化配置提供服务器和客户端支持。通过Config Server，您可以在所有环境中管理应用程序的外部属性。客户端和服务器上的概念与Spring Environment和PropertySource抽象，因此它们非常适合Spring应用程序，但可以与任何运行在任何语言的应用程序一起使用。随着应用程序从开发到测试转移到部署管道中，您可以管理这些环境之间的配置，并确保应用程序具有在迁移时所需运行的所有内容。服务器存储后端的默认实现使用git，因此它可以轻松支持配置环境的标签版本，并且可以用于管理内容的各种工具。使用Spring配置很容易添加替代实现并将其插入。

## 特征
Spring Cloud Config Server的特点：
	* HTTP，用于外部配置的资源API（名称 - 值对或同等YAML内容）
	* 加密和解密属性值（对称或不对称）
	* 使用可轻松嵌入Spring Boot应用程序 @EnableConfigServer配置客户端功能
	* 绑定到配置服务器并Environment使用远程属性来初始化Spring
	* 加密和解密属性值（对称或不对称）
	
## 快速开始
{% codeblock lang:java %}
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-config</artifactId>
            <version>2.0.0.M8</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-config</artifactId>
    </dependency>
</dependencies><repositories>
    <repository>
        <id>spring-milestones</id>
        <name>Spring Milestones</name>
        <url>https://repo.spring.io/libs-milestone</url>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
    </repository>
</repositories>
{% endcodeblock %}

只要Spring Boot Actuator和Spring Config Client位于类路径中，任何Spring Boot应用程序都会尝试联系配置服务器http://localhost:8888，默认值为 spring.cloud.config.uri。如果你想改变这个默认，你可以设置spring.cloud.config.uri在bootstrap.[yml | properties] 或通过系统属性或环境变量。
{% codeblock lang:java %}
@Configuration
@EnableAutoConfiguration
@RestController
public class Application {

  @Value("${config.name}")
  String name = "World";

  @RequestMapping("/")
  public String home() {
    return "Hello " + name;
  }

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }

}	
{% endcodeblock %}

案例当中config.name的值（或绑定到在Spring启动方式的任何其他值）可以来自本地配置或远程配置服务器。配置服务器默认优先。要/env在应用程序中查看此端点并查看configServer属性来源。

要运行您自己的服务器，请使用spring-cloud-config-server依赖关系和@EnableConfigServer。如果您设置spring.config.name=configserver应用程序将在端口8888上运行并提供示例存储库中的数据。您需要根据spring.cloud.config.server.git.uri自己的需要找到配置数据（默认情况下，它是git存储库的位置，可以是本地file:..URL）。

