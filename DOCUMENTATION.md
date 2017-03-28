[云框架]基于Spring Cloud的微服务架构 v0.1
===============

微服务架构（Microservices Architecture）是将应用拆分成小业务单元开发和部署，使用轻量级协议通信，通过协同工作实现应用逻辑的架构模式。

Spring Cloud是一个基于Spring Boot实现的云应用开发工具，是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。

尤其是对于JVM程序来说，Spring Cloud比Kubernetes更简单、易上手。

## 说明

+ [云框架]架构怎么做的？

### 架构图

+ 架构图

### 架构说明

+ [云框架]架构为什么要这么做？为什么这么做是最佳实践？

### 架构组件及关系说明

核心组件

<img src="./image/screenshot_1481715023954.png" width = "400" height = "400" alt="" align=center />

**+ Config**

> 配置管理开发工具包，可以让你把配置放到远程服务器，目前支持本地存储、Git以及Subversion

**+ Eureka**
  
> 云端负载均衡，一个基于 REST 的服务，用于定位服务，以实现云端的负载均衡和中间层服务器的故障转移
  
**+ Hystrix**
  
> 容错管理工具，旨在通过控制服务和第三方库的节点,从而对延迟和故障提供更强大的容错能力

**+ Zuul**

> 边缘服务工具，是提供动态路由，监控，弹性，安全等的边缘服务

**+ Feign**

> Feign是一种声明式、模板化的HTTP客户端

**+ Ribbon**

> 提供云端负载均衡，有多种负载均衡策略可供选择，可配合服务发现和断路器使用

**+ Sleuth**

> 日志收集工具包，封装了Dapper、Zipkin和HTrace操作


* 如何访问这些服务

<img src="./image/screenshot_1481696906259.png" width = "450" height = "300" alt="" align=center />

* 服务如何发现

<img src="./image/screenshot_1481696964742.png" width = "450" height = "300" alt="" align=center />


<img src="./image/screenshot_1481696995555.png" width = "450" height = "300" alt="" align=center />

* 服务如何通信

<img src="./image/screenshot_1481697051990.png" width = "450" height = "300" alt="" align=center />

* 数据如何管理

<img src="./image/screenshot_1481697088445.png" width = "450" height = "300" alt="" align=center />

* 服务如何容错

<img src="./image/screenshot_1481697117246.png" width = "450" height = "300" alt="" align=center />

* 服务如何监控

<img src="./image/screenshot_1481697160945.png" width = "450" height = "300" alt="" align=center />

### 适用场景

+ 大规模开发
+ 有业务模块松耦合需求
+ 现有业务开发迭代敏捷性低

## 使用

### 使用向导

#### 云帮部署

+ 第一步
+ 第二步
+ 第三步
+ ···

#### Dockerfile部署

+ 第一步
+ 第二步
+ 第三步
+ ···

### 高级

*该云框架的高级使用技巧

+ 高级操作1
+ 高级操作2
+ 高级操作3
+ ···

### 已知问题

*已知问题即目前知道但无法解决的问题

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

## 参考资料

+ [干货下载：谷歌、亚马逊等十大公司微服务案例精选](https://mp.weixin.qq.com/s?__biz=MzIwMDA2OTI0Mw==&mid=2653449136&idx=2&sn=0e6bc2215646064c9a35398a8fb00299&chksm=8d5e12a4ba299bb2bf75f5b8aebb645c186932b6507dbd2ca9372dbd5b0f4d0a5a43e9fce72d#rd)
+ [部署微服务：Spring Cloud vs. Kubernetes](http://www.jianshu.com/p/2f443a5a9d99)

## 更新日志

+ 2017.03.28 
  + 新增user-guide
+ [历史更新](CHANGLOG.md)

## 贡献者

`发起者` 张斌 [zhangb@goodrain.com](mailto:zhangb@goodrain.com) WeChat：elvis_123456

`贡献者` 孙丽川 [sunlc@goodrain.com](mailto:sunlc@goodrain.com) WeChat：

`贡献者` 田夜雨 [tianyy@goodrain.com](mailto:tianyy@goodrain.com) WeChat：yeyu_t

## 社区

+ [订阅邮件](http://goodrain.us15.list-manage.com/subscribe?u=1874f1de4ed82a52890cefb4c&id=b88f73ca56)
+ QQ群1: 531980120
+ 微信二维码
+ [联系我们](mailto:info@goodrain.com)

## 扩展链接

## 版权声明

云框架遵循APACHE LICENSE 2.0协议发布，并提供免费使用。

细节参阅 [LICENSE.md](链接)

-------

[云框架](README.md)，即插即用的云上技术框架。


==========
 
## 什么是微服务？
&emsp;&emsp;微服务架构（Microservices Architecture）是将应用拆分成小业务单元开发和部署，使用轻量级协议通信，通过协同工作实现应用逻辑的架构模式。
  
## 微服务特点
* 服务组件化－－应用拆分成不同服务运行在不同进程中，明确定义服务边界

* 按业务划分服务与组织－－业务领域的全栈（从前端到后端）软件实现

* 去中心化－－针对业务特征选择不同的技术水平，针对性的解决问题

* 设计失败－－服务的消费方需要优雅的处理错误

* 智能终端－－业务逻辑在服务内部处理；服务间通信尽轻量化，不添加任何额外的业务规则

* 自动化－－开发、调试、测试、集成、监控和发布

* API GateWay－－统一暴露服务接口；对服务认证、授权、监控、路由等

## 微服务如何落地
* 如何访问这些服务

<img src="./image/screenshot_1481696906259.png" width = "450" height = "300" alt="" align=center />

* 服务如何发现

<img src="./image/screenshot_1481696964742.png" width = "450" height = "300" alt="" align=center />


<img src="./image/screenshot_1481696995555.png" width = "450" height = "300" alt="" align=center />

* 服务如何通信

<img src="./image/screenshot_1481697051990.png" width = "450" height = "300" alt="" align=center />

* 数据如何管理

<img src="./image/screenshot_1481697088445.png" width = "450" height = "300" alt="" align=center />

* 服务如何容错

<img src="./image/screenshot_1481697117246.png" width = "450" height = "300" alt="" align=center />

* 服务如何监控

<img src="./image/screenshot_1481697160945.png" width = "450" height = "300" alt="" align=center />

## springcloud 是什么？
&emsp;&emsp;Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署


## springcloud 核心组件

<img src="./image/screenshot_1481715023954.png" width = "400" height = "400" alt="" align=center />

## 示例学习路径

<img src="./image/screenshot_method.png" width = "450" height = "400" alt="" align=center />


## 版权信息
  
云框架遵循APACHE LICENSE 2.0协议发布，并提供免费使用。
  
细节参阅 [LICENSE.md](链接)
