[![Goodrain Cloud Frameworks](http://7xihe6.com1.z0.glb.clouddn.com/CLOUDFRAMEWORKS9x3d.jpg)](http://app.goodrain.com)

# [云框架]基于Spring Cloud的微服务架构 v0.1

![](https://img.shields.io/badge/Version-0.1-brightgreen.svg)
![](https://img.shields.io/badge/License-APACHE2.0-blue.svg)

## 目录

* [背景](#背景)
* [说明](#说明)
  * [架构图](#架构图)
  * [架构说明](#架构说明)
  * [组件说明](#组件说明)
  * [组件关系](#组件关系)
  * [适用场景](#适用场景)  
* [使用](#使用)
  * [使用向导](#使用向导)
  * [高级操作](#高级操作)
  * [已知问题](#已知问题)
  * [性能测试](#性能测试)  
* [常见问题](#常见问题)
* [更新日志](#更新日志)
* [贡献者](#贡献者)
* [社区](#社区)
* [扩展阅读](#扩展阅读)
* [版权声明](#版权声明)

## <a name="背景"></a>背景

[Spring Cloud](http://projects.spring.io/spring-cloud/)是Pivotal提供的云应用开发工具，基于Spring Boot实现，用于简化分布式系统构建。

利用Spring Boot的开发便利性，Spring Cloud为JVM云应用开发中的配置管理、服务发现、断路器、智能路由、微代理、控制总线、全局锁、决策竞选、分布式会话和集群状态管理等操作提供了一种简单的实现方式。

相比Dubbo等RPC（远程过程调用协议）框架，Spring Cloud是一个比较新的微服务架构基础框架选择，2016年才推出的1.0 release版本，不过Spring Cloud的方案完整度非常高，各个子项目几乎覆盖了微服务架构的方方面面。

**Spring Cloud核心组件**

| 名称 | 功能 | 简介 |
| --- | --- | --- |
| Spring Cloud Config | 配置管理开发工具包 | 允许用户把配置放到远程服务器，支持本地存储、Git及Subversion |
| Netflix Eureka | 云端负载均衡 | 基于 REST 的服务，用于定位服务，以实现云端的负载均衡和中间层服务器的故障转移 |
| Netflix Hystrix | 容错管理工具 | 通过控制服务和第三方库的节点，从而对延迟和故障提供更强大的容错能力 |
| Netflix Zuul | 边缘服务工具 | 提供动态路由，监控，弹性，安全等的边缘服务 |
| Netflix Feign | 客户端 | 声明式、模板化的HTTP客户端 |
| Netflix Ribbon | 云端负载均衡 | 有多种负载均衡策略可供选择，可配合服务发现和断路器使用 |
| Spring Cloud Sleuth | 日志收集工具包 | 封装了Dapper、Zipkin和HTrace操作 |

## <a name="说明"></a>说明

### <a name="架构图"></a>架构图

### <a name="架构说明"></a>架构说明

### <a name="组件关系"></a>组件关系

### Q：如何访问这些服务？

<img src="./image/云框架-Spring Cloud-如何访问这些服务.png" width = "450" height = "" alt="" align=center />

### Q：服务如何发现？

<img src="./image/云框架-Spring Cloud-服务如何发现1.png" width = "450" height = "" alt="" align=center />

<img src="./image/云框架-Spring Cloud-服务如何发现2.png" width = "450" height = "" alt="" align=center />

### Q：服务如何通信？

<img src="./image/云框架-Spring Cloud-服务如何通信.png" width = "450" height = "" alt="" align=center />

### Q：数据如何管理？

<img src="./image/云框架-Spring Cloud-数据如何管理.png" width = "450" height = "" alt="" align=center />

### Q：服务如何容错？

<img src="./image/云框架-Spring Cloud-服务如何容错.png" width = "450" height = "" alt="" align=center />

### Q：服务如何监控？

<img src="./image/云框架-Spring Cloud-服务如何监控.png" width = "450" height = "" alt="" align=center />

### <a neme="组件说明"></a>组件说明

* [Spring Cloud Config - server](https://github.com/cloudframeworks-springcloud/config-client)
* [Spring Cloud Config - client](https://github.com/cloudframeworks-springcloud/config-server)
* [Netflix Eureka - server](https://github.com/cloudframeworks-springcloud/eureka-server)
* [Netflix Eureka - service](https://github.com/cloudframeworks-springcloud/eureka-service)
* [Netflix Hystrix](https://github.com/cloudframeworks-springcloud/hystrix)
* [Netflix Zuul](https://github.com/cloudframeworks-springcloud/zuul)
* [Netflix Feign](https://github.com/cloudframeworks-springcloud/feign)
* [Netflix Ribbon](https://github.com/cloudframeworks-springcloud/ribbon)
* [Spring Cloud Sleuth](https://github.com/cloudframeworks-springcloud/sleuth)

### <a name="适用场景"></a>适用场景

+ 大规模开发
+ 有业务模块松耦合需求
+ 现有业务开发迭代敏捷性低

## <a name="使用"></a>使用

### <a name="使用向导"></a>使用向导

+ 第一步
+ 第二步
+ 第三步
+ ···

### <a name="高级操作"></a>高级操作

+ 高级操作1
+ 高级操作2
+ 高级操作3
+ ···

### <a name="已知问题"></a>已知问题

+ 已知问题1
+ 已知问题2
+ 已知问题3
+ ···

### <a name="性能测试"></a>性能测试

## <a name="常见问题"></a>常见问题

* [Spring Cloud Config - server](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Spring%20Cloud%20Config%20-%20server)
* [Spring Cloud Config - client](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Spring%20Cloud%20Config%20-%20client)
* [Netflix Eureka - server](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Netflix%20Eureka%20-%20server)
* [Netflix Eureka - service](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Netflix%20Eureka%20-%20service)
* [Netflix Hystrix](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Netflix%20Hystrix)
* [Netflix Zuul](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Netflix%20Zuul)
* [Netflix Feign](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Netflix%20Feign)
* [Netflix Ribbon](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Netflix%20Ribbon)
* [Spring Cloud Sleuth](https://github.com/cloudframeworks-springcloud/user-guide/blob/master/QA/Spring%20Cloud%20Sleuth)

## <a name="更新日志"></a>更新日志

+ 2017.03.28 
  + 新增user-guide
+ [历史更新](CHANGLOG.md)

## <a name="贡献者"></a>贡献者

`出品人` 张斌 [zhangb@goodrain.com](mailto:zhangb@goodrain.com) WeChat：elvis_123456

`贡献者` 孙丽川 [sunlc@goodrain.com](mailto:sunlc@goodrain.com) WeChat：linmu0001

`贡献者` 田夜雨 [tianyy@goodrain.com](mailto:tianyy@goodrain.com) WeChat：yeyu_t

## <a name="社区"></a>社区

+ [订阅邮件](http://goodrain.us15.list-manage.com/subscribe?u=1874f1de4ed82a52890cefb4c&id=b88f73ca56)
+ QQ群1: 531980120
+ 微信二维码（发布时补充）
+ [联系我们](mailto:info@goodrain.com)

## <a name="扩展阅读"></a>扩展阅读

+ [Microservices by Martin Flowler](https://martinfowler.com/articles/microservices.html)
+ [部署微服务：Spring Cloud vs. Kubernetes](http://www.jianshu.com/p/2f443a5a9d99)
+ [干货下载：谷歌、亚马逊等十大公司微服务案例精选](https://mp.weixin.qq.com/s?__biz=MzIwMDA2OTI0Mw==&mid=2653449136&idx=2&sn=0e6bc2215646064c9a35398a8fb00299&chksm=8d5e12a4ba299bb2bf75f5b8aebb645c186932b6507dbd2ca9372dbd5b0f4d0a5a43e9fce72d#rd)

## <a name="版权声明"></a>版权声明

云框架遵循APACHE LICENSE 2.0协议发布，并提供免费使用。

细节参阅 [LICENSE.md](链接)

-------

[云框架](ABOUT.md)，即插即用的云端技术框架。
