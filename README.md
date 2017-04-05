# [云框架]基于Spring Cloud的微服务架构 v0.1

![](https://img.shields.io/badge/build-passing-green.svg)
![](https://img.shields.io/badge/release-v0.1-red.svg)
[![](https://img.shields.io/badge/CHANGELOG-v0.1-yellow.svg)](CHANGELOG.md)
![](https://img.shields.io/badge/License-Apache_2.0-blue.svg)
[![](https://img.shields.io/badge/Prodcuer-Bin%20Zhang-orange.svg)](CONTRIBUTORS.md)

[微服务](https://martinfowler.com/articles/microservices.html)架构近年来受到了众多开发者的追捧。相比传统架构模式，微服务架构具有语言无关性、独立进程通讯、高度解耦、任务边界固定、按需扩展等特点，非常适合互联网公司快速交付、响应变化、不断试错的需求，也因此受到了像Twitter、Netflix、Amazon、eBay这样的科技巨头的青睐（[案例](https://mp.weixin.qq.com/s?__biz=MzIwMDA2OTI0Mw==&mid=2653449136&idx=2&sn=0e6bc2215646064c9a35398a8fb00299&chksm=8d5e12a4ba299bb2bf75f5b8aebb645c186932b6507dbd2ca9372dbd5b0f4d0a5a43e9fce72d#rd)）。

目前主流微服务框架包括Spring Cloud、Dubbo、API Gateway等，其中[Spring Cloud](http://projects.spring.io/spring-cloud/)是Pivotal提供的云应用开发工具，利用Spring Boot的开发便利性，Spring Cloud为JVM云应用开发中的配置管理、服务发现、断路器、智能路由、微代理、控制总线、全局锁、决策竞选、分布式会话和集群状态管理等操作提供了一种简单的实现方式。

相比Dubbo等RPC（远程过程调用协议）框架，Spring Cloud是一个比较新的微服务架构基础框架选择，2016年才推出的1.0 release版本，不过Spring Cloud的方案完整度非常高，各个子项目几乎覆盖了微服务架构的方方面面。从目前的关注度和活跃度来看，Spring Cloud很可能会成为微服务架构的标准。

本篇[**[云框架]**](ABOUT.md)目的不在于重复造轮（[Spring Cloud官方文档](https://spring.io/docs)），而是总结过去数十个微服务架构项目落地的成功经验，为开发者提供**基于Spring Cloud的微服务架构**的最佳实践。不必从零开始开发，开发者仅需在[云框架]基础上替换部分业务代码，就可以将基于Spring Cloud的微服务架构应用于生产环境并立即产生价值。

如果你是初学者，可顺序阅读操作，快速上手；如果你想要快速部署，可跳转至[一条命令部署](#一条命令部署)。

## 内容概览

* [DEMO演示](#DEMO演示)
* [组件说明](#组件说明) 
* [使用向导](#使用向导)
* [常见问题](#常见问题)
* [参与贡献](#参与贡献)
* [加入社群](#加入社群)
* [扩展阅读](#扩展阅读)

## <a name="DEMO演示"></a>DEMO演示

## <a name="组件说明"></a>组件说明

### <a name="架构图"></a>架构图

<div align=center><img width="900" height="" src="./image/云框架-Spring Cloud-架构图.png"/></div>

* 实线箭头：注册
* 虚线箭头：调用

***建议学习路径***

<div align=center><img width="900" height="" src="./image/云框架-Spring Cloud-学习路径.png"/></div>

### <a neme="组件说明"></a>组件说明

***点击[组件名称](#组件名称)跳转至组件源码***

| <a name="组件名称"></a>核心组件 | 功能 | 简介 |
| --- | --- | --- |
| [Spring Cloud Config - server](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client) | 配置管理开发工具包 | 允许用户把配置放到远程服务器，支持本地存储、Git及Subversion |
| [Spring Cloud Config - client](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server) |  |   |
| [Spring Cloud Config - 配置文件](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config) |  |  |
| [Netflix Eureka - server](https://github.com/cloudframeworks-springcloud/Netflix-Eureka-server) | 云端负载均衡 | 基于REST的服务，用于定位服务，以实现云端的负载均衡和中间层服务器的故障转移 |
| [Netflix Eureka - service](https://github.com/cloudframeworks-springcloud/Netflix-Eureka-service) |  |  |
| [Netflix Hystrix](https://github.com/cloudframeworks-springcloud/Netflix-Hystrix) | 容错管理工具 | 通过控制服务和第三方库的节点，从而对延迟和故障提供更强大的容错能力 |
| [Netflix Zuul](https://github.com/cloudframeworks-springcloud/Netflix-Zuul) | 边缘服务工具 | 提供动态路由，监控，弹性，安全等的边缘服务 |
| [Netflix Feign](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Feign) | 客户端 | 声明式、模板化的HTTP客户端 |
| [Netflix Ribbon](https://github.com/cloudframeworks-springcloud/Netflix-Ribbon) | 云端负载均衡 | 有多种负载均衡策略可供选择，可配合服务发现和断路器使用 |
| [Spring Cloud Sleuth](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Sleuth) | 日志收集工具包 | 封装了Dapper、Zipkin和HTrace操作 |

## <a name="使用向导"></a>使用向导

### <a name="一条命令部署"></a>一条命令部署



### <a name="高级操作"></a>高级操作

* [Spring Cloud Config](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/components%20wizards/Spring%20Cloud%20Config.md)
* [Netflix Eureka](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/components%20wizards/Netflix%20Eureka.md)
* [Netflix Feign](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/components%20wizards/Netflix%20Feign.md)
* [Netflix Hystrix](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/components%20wizards/Netflix%20Hystrix.md)
* [Netflix Ribbon](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/components%20wizards/Netflix%20Ribbon.md)
* [Netflix Zuul](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/components%20wizards/Netflix%20Zuul.md)
* [Spring Cloud Sleuth](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/components%20wizards/Spring%20Cloud%20Sleuth.md)

### <a name="可用性测试"></a>可用性测试

## <a name="常见问题"></a>常见问题

相关问题可通过[GitHub ISSUE](https://github.com/cloudframeworks-springcloud/user-guide/issues)提交或讨论，点击查看[常见问题汇总](QA.md)

## <a name="社区"></a>社区

+ [订阅邮件](http://goodrain.us15.list-manage.com/subscribe?u=1874f1de4ed82a52890cefb4c&id=b88f73ca56)
+ QQ群1: 531980120
+ 微信二维码（发布时补充）
+ [联系我们](mailto:info@goodrain.com)

## <a name="扩展阅读"></a>扩展阅读

+ [Microservices by Martin Fowler](https://martinfowler.com/articles/microservices.html)
+ [Microservices Resource Guide by Martin Fowler](https://martinfowler.com/microservices/)
+ [部署微服务：Spring Cloud vs. Kubernetes](http://www.jianshu.com/p/2f443a5a9d99)
+ [干货下载：谷歌、亚马逊等十大公司微服务案例精选](https://mp.weixin.qq.com/s?__biz=MzIwMDA2OTI0Mw==&mid=2653449136&idx=2&sn=0e6bc2215646064c9a35398a8fb00299&chksm=8d5e12a4ba299bb2bf75f5b8aebb645c186932b6507dbd2ca9372dbd5b0f4d0a5a43e9fce72d#rd)

-------

[云框架](ABOUT.md)系列主题，遵循[APACHE LICENSE 2.0](LICENSE.md)协议发布。
