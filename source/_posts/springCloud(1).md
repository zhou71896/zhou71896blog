---
title: SpringCloud的基本介绍
date: 2018-03-19 10:03:42
tags:
---
# 一.springCloud简介

Spring Cloud为开发人员提供了快速构建分布式系统中一些常见模式的工具（例如配置管理，服务发现，断路器，智能路由，微代理，控制总线，一次性令牌，全局锁定，领导选举，分布式会话，群集状态）。分布式系统的协调导致锅炉板模式，使用Spring Cloud开发人员可以快速站出实现这些模式的服务和应用程序。他们可以在任何分布式环境中运行良好，包括开发人员自己的笔记本电脑，裸机数据中心和托管平台，如Cloud Foundry。

# 二.springCloud的相关特征

Spring Cloud专注于为典型用例和可扩展性机制提供良好的即时体验，以覆盖其他人。
	* 分布式/版本化配置
	* 服务注册和发现
	* 路由
	* 服务对服务呼叫
	* 负载均衡
	* 断路器
	* 全局锁定
	* 领导选举和集群状态
	* 分布式消息
	
# 三.主要项目
SpringCloud 配置
由git存储库支持的集中式外部配置管理。配置资源直接映射到`Spring Environment`，但如果需要可以由非Spring应用程序使用。

SpringCloudNetflix
与各种Netflix OSS组件(Eureka, Hystrix,Zuul,Archaius等)集成。

SpringCloudBus
用于将服务和服务实例与分布式消息一起链接的事件总线。用于跨集体传播状态更改(例如配置更改事件)。

CludFoundry的SpringCloud
将您的应用程序与PivotalCloudFoundry集成。提供服务发现实现，还可以轻松实现SSO和OAuth2保护的资源。

SpringCloud开放式服务代理
为构建实现OpenServiceBroker API的服务代理提供了一个起点。

Spring云群集
领导选举
和常见的有状态模式,为Zookeeper,Redis,Hazelcast,Consul提供和实施。

Spring Cloud Consul
与Hashicorp Consul进行服务发现和配置管理。

Spring Cloud安全
为Zuul代理中的负载均衡OAuth2休息客户端和身份验证报头中继提供支持。

Spring Cloud Sleuth(Spring云侦探)
Spring Cloud应用程序的分布式跟踪，与Zipkin,HTrance和基于日志的(列如ELK)跟踪兼容

Spring云数据流
现代运行时组合式微服务应用程序的云本地编排服务。易于使用的DSL，拖方式的GUI和REST-API一起简化了基于微服务的数据管道的整体编排

Spring Cloud Data Flow(Spring云数据流)
现代运行时组合式服务应用程序的云本地编排服务。易于使用的DSL,拖方式GUI和REST-API一起简化了基于微服务的数据管道的整体编排。

Spring Cloud Stream
轻量级事件驱动的微服务框架，可快速构建可连接到外部系统的应用程序。使用Apache Kafka或RabbitMQ在SpringBoot应用程序之间发送和接收消息的简单声明模型。

Spring Cloud Stream 应用程序启动器
SpringCloudStreamAppStarters是基于SpringBootIntergration应用程序,可与外部系统集成。

Spring Cloud Task
一个短生命周期的微服务框架，用于快速构建执行有限数据处理的应用程序。向SpringBoot应用程序添加功能性和非功能性功能的简单声明。

Spring Cloud Task App Starter
SpringCloud任务应用程序启动器是SpringBoot应用程序，可能是任何进程，包括不能永久运行的SpringBatch作业,并且会在有限的数据处理期结束/停止。

Spring Cloud ZooKeeper
使用ApacheZookeeper进行服务发现和配置管理。

Spring Cloud for Amazon Web Services 
与托管的AmazonWebServices轻松集成。它提供了一种使用众所周知的Spring接口和API(如消息传递或者缓存API)与AWS提供的服务进行交互的便捷方式。开发人员可以围绕托管服务构建应用程序，而无需关心基础框架或维护。

Spring Cloud Connectors
让各种平台上的PaaS应用程序轻松连接到后端服务，如数据库和消息代理（该项目以前称为“Spring Cloud”）。

Spring Cloud Starters
Spring Boot式初学者项目，可以减轻Spring Cloud消费者的依赖性管理。（作为一个项目终止并与Angel.SR2之后的其他项目合并。）

Spring Cloud CLI
SPring BOot CLI 插件，用于在Groovy中快速创建Spring Cloud组件应用程序

Spring Cloud Contract
Spring Cloud Contract是一个涵盖各种解决方案的综合项目,可帮助用户成功实施消费者驱动合同方法。

Spring Cloud Gateway(SpringCloud网关)
Spring Cloud Gateway是基于ProjectReactor的只能可编程路由器。

Spring Cloud OpenFegin
Spring Cloud OpenFegin通过自动配置和绑定到SpringEnvironment和其他Spring编程模型成语来为SpringBoot应用程序提供集成。



