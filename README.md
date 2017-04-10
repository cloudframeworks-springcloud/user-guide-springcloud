# [云框架]基于Spring Cloud的微服务架构 v0.1

![](https://img.shields.io/badge/build-passing-green.svg)
![](https://img.shields.io/badge/release-v0.1-red.svg)
[![](https://img.shields.io/badge/CHANGELOG-v0.1-yellow.svg)](CHANGELOG.md)
![](https://img.shields.io/badge/License-Apache_2.0-blue.svg)
[![](https://img.shields.io/badge/Prodcuer-Bin%20Zhang-orange.svg)](CONTRIBUTORS.md)

[微服务](https://martinfowler.com/articles/microservices.html)近年来受到了众多开发者的追捧。相比传统架构模式，微服务架构具有语言无关性、独立进程通讯、高度解耦、任务边界固定、按需扩展等特点，非常适合互联网公司快速交付、响应变化、不断试错的需求，也因此受到了像Twitter、Netflix、Amazon、eBay这样的科技巨头的青睐（[案例](https://mp.weixin.qq.com/s?__biz=MzIwMDA2OTI0Mw==&mid=2653449136&idx=2&sn=0e6bc2215646064c9a35398a8fb00299&chksm=8d5e12a4ba299bb2bf75f5b8aebb645c186932b6507dbd2ca9372dbd5b0f4d0a5a43e9fce72d#rd)）。

目前主流微服务框架包括Spring Cloud、Dubbo、API Gateway等，其中[Spring Cloud](http://projects.spring.io/spring-cloud/)是Pivotal提供的云应用开发工具，利用Spring Boot的开发便利性，Spring Cloud为JVM云应用开发中的配置管理、服务发现、断路器、智能路由、微代理、控制总线、全局锁、决策竞选、分布式会话和集群状态管理等操作提供了一种简单的实现方式。

相比Dubbo等RPC（远程过程调用协议）框架，Spring Cloud是一个比较新的微服务架构基础框架选择，2016年才推出的1.0 release版本，不过Spring Cloud的方案完整度非常高，各个子项目几乎覆盖了微服务架构的方方面面。从目前的关注度和活跃度来看，Spring Cloud很可能会成为微服务架构的标准。

本篇[云框架](ABOUT.md)目的不在于重复造轮，而是总结过去数十个微服务架构项目的成功经验，绕过前人踩过的坑，以一个实际项目（[PiggyMetrics](https://github.com/sqshq/PiggyMetrics)，一款个人财务管理应用）为例，为开发者提供微服务落地的最佳实践。

不必从零开始开发，开发者仅需在[云框架]基础上替换部分业务代码，就可以将[基于Spring Cloud的微服务架构](README.md)应用于生产环境并立即产生价值。

# 内容概览

* [快速部署](#快速部署)
* [组件说明](#组件说明) 
* [常见问题](#常见问题)
* [更新计划](#更新计划)
* [参与贡献](#参与贡献)
* [加入社群](#加入社群)

# <a name="快速部署"></a>快速部署

* 准备工作
* 操作步骤

# <a name="组件说明"></a>组件说明

Piggymetrics（[查看应用](http://my-piggymetrics.rhcloud.com/)）由统计服务（STATISTICS SERVICE）、账户服务（ACCOUNT SERVICE）、通知服务（NOTIFICATION SERVICE）等三个核心微服务组成：

* 每个微服务都是围绕业务能力组织的可独立部署的应用程序，
* 每个微服务都拥有独立的数据库（MangoDB，支持多种编程语言持久性架构）
* 微服务与微服务之间通信使用同步的REST API

PiggyMetrics基础服务设施中用到了Spring Cloud Config、Netflix Eureka、Netflix Hystrix、Netflix Zuul、Netflix Ribbon等组件，而这也正是Spring Cloud分布式开发中最核心的5个组件。

<div align=center><img width="900" height="" src="./image/piggymetrics.png"/></div>

### Spring Cloud Config

[[使用向导]](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/components%20wizards/Spring%20Cloud%20Config.md)[[client-配置说明]](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client)[[server-配置说明]](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server)[[config-配置说明]](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config)

### Netflix Zuul



### Netflix Eureka

### Netflix Ribbon

### Netflix Hystrix

### Netflix Feign

# <a name="常见问题"></a>常见问题

任何相关问题均可通过[GitHub ISSUE](https://github.com/cloudframeworks-springcloud/user-guide/issues)提交或讨论，问题总结请查看[[QA](QA.md)]

# <a name="更新计划"></a>更新计划

* 增加在线演示
* 增加TURBINE组件说明
* 增加CI/CD、日志实现方法
* 增加云帮部署

# <a name="参与贡献"></a>参与贡献

[如何成为云框架贡献者](CONTRIBUTING.md)

# <a name="加入社群"></a>加入社群

+ [订阅邮件](http://goodrain.us15.list-manage.com/subscribe?u=1874f1de4ed82a52890cefb4c&id=b88f73ca56)
+ QQ群1: 531980120
+ 微信二维码（发布时补充）
+ [联系我们](mailto:info@goodrain.com)

-------

[云框架](ABOUT.md)系列主题，遵循[APACHE LICENSE 2.0](LICENSE.md)协议发布。
