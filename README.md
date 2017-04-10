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
* [框架说明](#框架说明) 
  * [架构图](#架构图)
  * [组件说明](#组件说明)
* [常见问题](#常见问题)
* [更新计划](#更新计划)
* [参与贡献](#参与贡献)
* [加入社群](#加入社群)

# <a name="快速部署"></a>快速部署

* 开发环境（准备工作、操作步骤）
* 生产环境（准备工作、操作步骤）

# <a name="框架说明"></a>框架说明

Piggymetrics（[查看应用](http://my-piggymetrics.rhcloud.com/)）由统计服务（[STATISTICS SERVICE](https://github.com/sqshq/PiggyMetrics#statistics-service)）、账户服务（[ACCOUNT SERVICE](https://github.com/sqshq/PiggyMetrics#account-service)）、通知服务（[NOTIFICATION SERVICE](https://github.com/sqshq/PiggyMetrics#notification-service)）等三个核心微服务组成，其中：

* 每个微服务都是围绕业务能力组织的可独立部署的应用程序
* 每个微服务都拥有独立的数据库（MangoDB，支持多种编程语言持久性架构）
* 微服务与微服务之间通信使用同步的REST API

PiggyMetrics基础服务设施中用到了Spring Cloud Config、Netflix Eureka、Netflix Hystrix、Netflix Zuul、Netflix Ribbon等组件，而这也正是Spring Cloud分布式开发中最核心的5个组件。

## <a name="架构图"></a>架构图

<div align=center><img width="900" height="" src="./image/piggymetrics.png"/></div>

## <a name="组件说明"></a>组件说明

### Spring Cloud Config

Spring Cloud Config提供解决分布式系统的配置管理方案，分server、client两个模块：

* config_server 配置服务器：统一配置系统中需要的各种服务
* config_client 配置客户端：根据Spring框架的Environment和PropertySource从spring cloud config sever获取各种配置

Spring Cloud Config基于使用中心配置仓库的思想（版本控制），支持Git（默认）、SVN、File等三种储存方式。

#### 使用向导

1. 
2.
3.
4.
5.

#### 完整代码



#### 业务代码



#### 原始框架

[Spring Cloud Config - server](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server) • [Spring Cloud Config - client](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client) • [Spring Cloud Config - 配置文件](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client)

### Netflix Zuul

Netflix Zuul提供动态路由、监控、弹性、安全等的边缘服务。

在通过服务网关统一向外的提供REST API的微服务架构中，Netflix Zuul为微服务机构提供了前门保护的作用，同时将权限控制这些较重的非业务逻辑内容迁移到服务路由层面，使得服务集群主体能够具备更高的可复用性和可测试性。

#### 使用向导

1. 
2.
3.
4.
5.

#### 完整代码



#### 业务代码



#### 原始框架

[Netflix Zuul](https://github.com/cloudframeworks-springcloud/Netflix-Zuul)

### Netflix Eureka

相比传统SOA架构，微服务架构中的服务粒度更小、服务数量更多，如何有效管理各个服务就显得尤为重要，也因此出现了服务注册的概念。

服务注册的本质：1）简单易用，对用户透明；2）高可用，满足CAP理论；3）多语言支持

在基于Spring Cloud的微服务架构中，通常采用Netflix Eureka作为注册中心，某些情况下也会采用Zookeeper作为替代。

Netflix Eureka的易用性体现在两方面：

* 通过与Spring Boot(Cloud)结合达到只用注解和Maven依赖即可部署和启动服务的效果
* Netflix Eureka自带Client包，使得使用Eureka作为注册中心的客户端（即服务）不需要关心自己与Eureka的通讯机制，只需要引入Client依赖即可，当然前提是使用Java

**Netflix Eureka通过“伙伴”机制实现高可用**，每一台Eureka都需要在配置中指定另一个Eureka的地址作为伙伴，Eureka启动时会向自己的伙伴节点获取当前已经存在的注册列表，这样在向Eureka集群中增加新机器时就不需要担心注册列表不完整的问题，在CAP理论中满足AP原则。

除此之外，**Netflix Eureka支持Region和Zone的概念**，其中一个Region可以包含多个Zone。Eureka在启动时需要指定一个Zone名，即指定当前Eureka属于哪个Zone, 如果不指定则属于defaultZone。值得注意的是，Eureka Client也需要指定Zone。

Netflix Eureka使用Java编写，但它会将所有注册信息和心跳连接地址都暴露为HTTP REST接口，客户端实际是通过HTTP请求与Server进行通讯的，因此Client完全可以使用其它语言进行编写，只需要即时调用注册服务、注销服务、获取服务列表和心跳请求的HTTP REST接口即可。

#### 使用向导

1. 
2.
3.
4.
5.

#### 完整代码

#### 业务代码

#### 原始框架

[Netflix Eureka - server](https://github.com/cloudframeworks-springcloud/Netflix-Eureka-server) • [Netflix Eureka - service](https://github.com/cloudframeworks-springcloud/Netflix-Eureka-service)

### Netflix Ribbon

简单来说，Netflix Ribbon是一个客户端负载均衡器，有多种负载均衡策略可选（包括自定义的负载均衡算法），并可配合服务发现及断路器使用。在配置文件中列出Load Balancer后面所有的机器，Ribbon会自动的帮助你基于某种规则（如简单轮询，随机连接等）去连接这些机器。

#### 使用向导

1. 
2.
3.
4.
5.

#### 完整代码



#### 业务代码



#### 原始框架

[Netflix Ribbon](https://github.com/cloudframeworks-springcloud/Netflix-Ribbon)


### Netflix Hystrix

Netflix Hystrix是微服务分布式系统的熔断保护中间件，通过熔断机制控制服务和第三方库的节点，从而对延迟和故障提供更强大的容错能力。

#### 使用向导

1. 
2.
3.
4.
5.

#### 完整代码



#### 业务代码



#### 原始框架

[Netflix Hystrix](https://github.com/cloudframeworks-springcloud/Netflix-Hystrix)

### Netflix Feign

Spring Cloud集成Netflix Ribbon和Netflix Eureka提供的负载均衡的HTTP客户端Netflix Feign.

Netflix Feign是一个声明式、模板化的HTTP客户端，因此编写起来会更容易一些。Spring Cloud集成了Netflix Feign，并通过Netflix Ribbon和Netflix Eureka提供负载均衡。

使用Netflix Feign创建一个接口并对它进行注解（可插拔的注解支持，包括Feign注解），在应用主类中通过`@EnableFeignClients`注解开启Feign功能，并使用`@FeignClient`(服务ID)注解来绑定该接口对应服务。

#### 使用向导

1. 
2.
3.
4.
5.

#### 完整代码



#### 业务代码



#### 原始框架

[Netflix Feign](https://github.com/cloudframeworks-springcloud/Netflix-Feign)

### Spring Cloud Sleuth

Spring Cloud Sleuth是日志手机工具包，其中封装了Zipkin、HTrace和log-based追踪。

#### 使用向导

1. 
2.
3.
4.
5.

#### 完整代码



#### 业务代码



#### 原始框架

[Spring Cloud Sleuth](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Sleuth)

# <a name="常见问题"></a>常见问题

任何相关问题均可通过[GitHub ISSUE](https://github.com/cloudframeworks-springcloud/user-guide/issues)提交或讨论，问题总结请查看[[QA](QA.md)]

# <a name="更新计划"></a>更新计划

* 增加Turbine、Consul组件
* 增加CI/CD、日志监控实现方案
* 增加好雨云帮部署
* 增加云框架在线演示

# <a name="参与贡献"></a>参与贡献

[如何成为云框架贡献者](CONTRIBUTING.md)

# <a name="加入社群"></a>加入社群

+ [订阅邮件](http://goodrain.us15.list-manage.com/subscribe?u=1874f1de4ed82a52890cefb4c&id=b88f73ca56)
+ QQ群1: 531980120
+ 微信二维码（发布时补充）
+ [联系我们](mailto:info@goodrain.com)

-------

[云框架](ABOUT.md)系列主题，遵循[APACHE LICENSE 2.0](LICENSE.md)协议发布。
