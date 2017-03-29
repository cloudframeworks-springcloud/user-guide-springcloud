<h1 align=center><a href="http://www.goodrain.com/" title="Goodrain Cloudframeworks"><img style="float: left" width="900" src="http://7xihe6.com1.z0.glb.clouddn.com/CLOUDFRAMEWORKS9x3.jpg" alt="Goodrain Cloudframeworks logo"/></a></h1>

# [云框架]基于Spring Cloud的微服务架构 v0.1


Spring Cloud是Pivotal提供的云应用开发工具，基于Spring Boot实现，用于简化分布式系统构建。

利用Spring Boot的开发便利性，Spring Cloud为JVM云应用开发中的配置管理、服务发现、断路器、智能路由、微代理、控制总线、全局锁、决策竞选、分布式会话和集群状态管理等操作提供了一种简单的实现方式。

相比Dubbo等RPC（远程过程调用协议）框架，Spring Cloud是一个比较新的微服务架构基础框架选择，2016年才推出的1.0 release版本，不过Spring Cloud的方案完整度非常高，各个子项目几乎覆盖了微服务架构的方方面面。

Spring Cloud核心组件包括Spring Cloud Config、Netflix Eureka、Netflix Ribbon、Netflix Hystrix、Netflix Zuul等。

<img src="./image/云框架-Spring Cloud-核心组件.png" width = "450" height = "" alt="" align=center />

| 名称 | 功能 | 简介 |
| --- | --- | --- |
| Spring Cloud Config | 配置管理开发工具包 | 允许用户把配置放到远程服务器，支持本地存储、Git及Subversion |
| Netflix Eureka | 云端负载均衡 | 基于 REST 的服务，用于定位服务，以实现云端的负载均衡和中间层服务器的故障转移 |
| Netflix Hystrix | 容错管理工具 | 通过控制服务和第三方库的节点，从而对延迟和故障提供更强大的容错能力 |
| Netflix Zuul | 边缘服务工具 | 提供动态路由，监控，弹性，安全等的边缘服务 |
| Netflix Feign | 客户端 | 声明式、模板化的HTTP客户端 |
| Netflix Ribbon | 云端负载均衡 | 有多种负载均衡策略可供选择，可配合服务发现和断路器使用 |
| Spring Cloud Sleuth | 日志收集工具包 | 封装了Dapper、Zipkin和HTrace操作 |

## 说明

+ [云框架]架构怎么做的？

### 架构图

+ 架构图

<img src="./image/云框架-Spring Cloud-学习路径.png" width = "450" height = "" alt="" align=center />

### 架构说明

+ [云框架]架构为什么要这么做？为什么这么做是最佳实践？

### 关系说明

* **如何访问这些服务**

<img src="./image/云框架-Spring Cloud-如何访问这些服务.png" width = "450" height = "" alt="" align=center />

* **服务如何发现**

<img src="./image/云框架-Spring Cloud-服务如何发现1.png" width = "450" height = "" alt="" align=center />

<img src="./image/云框架-Spring Cloud-服务如何发现2.png" width = "450" height = "" alt="" align=center />

* **服务如何通信**

<img src="./image/云框架-Spring Cloud-服务如何通信.png" width = "450" height = "" alt="" align=center />

* **数据如何管理**

<img src="./image/云框架-Spring Cloud-数据如何管理.png" width = "450" height = "" alt="" align=center />

* **服务如何容错**

<img src="./image/云框架-Spring Cloud-服务如何容错.png" width = "450" height = "" alt="" align=center />

* **服务如何监控**

<img src="./image/云框架-Spring Cloud-服务如何监控.png" width = "450" height = "" alt="" align=center />

### 适用场景

+ 大规模开发
+ 有业务模块松耦合需求
+ 现有业务开发迭代敏捷性低

## 使用

### 使用向导

#### 部署方式1

+ 第一步
+ 第二步
+ 第三步
+ ···

### 高级

+ 高级操作1
+ 高级操作2
+ 高级操作3
+ ···

### 已知问题

+ 已知问题1
+ 已知问题2
+ 已知问题3
+ ···

### 性能测试

如何进行性能测试？性能标准？

## 常见问题

*常见问题指阅读／使用过程中经常会问的问题

+ Q：
  
  A：
  
+ Q：
  
  A：
  
+ ···

## 更新日志

+ 2017.03.28 
  + 新增user-guide
+ [历史更新](CHANGLOG.md)

## 贡献者

`出品人` 张斌 [zhangb@goodrain.com](mailto:zhangb@goodrain.com) WeChat：elvis_123456

`贡献者` 孙丽川 [sunlc@goodrain.com](mailto:sunlc@goodrain.com) WeChat：

`贡献者` 田夜雨 [tianyy@goodrain.com](mailto:tianyy@goodrain.com) WeChat：yeyu_t

## 社区

+ [订阅邮件](http://goodrain.us15.list-manage.com/subscribe?u=1874f1de4ed82a52890cefb4c&id=b88f73ca56)
+ QQ群1: 531980120
+ 微信二维码（发布时补充）
+ [联系我们](mailto:info@goodrain.com)

## 扩展阅读

+ [干货下载：谷歌、亚马逊等十大公司微服务案例精选](https://mp.weixin.qq.com/s?__biz=MzIwMDA2OTI0Mw==&mid=2653449136&idx=2&sn=0e6bc2215646064c9a35398a8fb00299&chksm=8d5e12a4ba299bb2bf75f5b8aebb645c186932b6507dbd2ca9372dbd5b0f4d0a5a43e9fce72d#rd)
+ [部署微服务：Spring Cloud vs. Kubernetes](http://www.jianshu.com/p/2f443a5a9d99)

## 版权声明

云框架遵循APACHE LICENSE 2.0协议发布，并提供免费使用。

细节参阅 [LICENSE.md](链接)

-------

<h1><a href="http://www.goodrain.com/" title="Goodrain Cloudframeworks"><img style="float: left" width="360" src="http://7xihe6.com1.z0.glb.clouddn.com/CLOUDFRAMEWORKS  header.jpg" alt="Goodrain Cloudframeworks logo"/></a></h1>

云框架（Cloud Frameworks）是即插即用的云端技术框架，使用Git控制版本，目前托管在GitHub上。

云框架具备可复用性和可定制性，有代码和文档可以看，有完整demo可以参考，并提供多种向导式部署和使用方式。

## 特性简介

### 实用干货

主题覆盖各类精选技术场景，内容清晰实用；

### 快速学习

没有太高的技术门槛，参照架构图及使用向导，零基础用户也可在边用边学的过程中快速掌握前沿技术；

### 即插即用

仅需替换部分业务代码，即可将技术应用于生产环境，并立即产生价值；

### 最佳实践

总结前人经验，萃取最佳实践，避免重复踩坑；

## 快速上手

### 目录结构

```
Cloud frameworks
|-- user-guide
    |--README.md
    |--CHANGELOG.md
    |--LICENSE.md
    |--CONTRIBUTING.md
    |--DOCUMENTATION.md
    |--images
|-- 组件1
|-- 组件2
|-- 组件3
`-- 组件n      
```

### user-guide

云框架主题展现为Github上的组织（organization），组织中仓库（repository）包括“user-guide”及一个或多个“组件”。

在user-guide仓库中，你可以很方便的找到帮助了解和使用云框架的文档，并根据“DOCUMENTATION.md”快速开始。

## 参与贡献

[如何成为云框架贡献者？](CONTRIBUTING.md)

## 版权信息

云框架遵循APACHE LICENSE 2.0协议发布，并提供免费使用。

细节参阅 [LICENSE](LICENSE.md)
