# 常见问题

### 服务如何访问？

<div align=center><img width="900" height="" src="./image/如何访问这些服务.png"/></div>

### 服务如何发现？

<div align=center><img width="900" height="" src="./image/服务如何发现1.png"/></div>

<div align=center><img width="900" height="" src="./image/服务如何发现2.png"/></div>

### 服务如何通信？

|  | 一对一 | 一对多 |
| --- | --- | --- |
| 同步 | 请求／响应 | ——— |
| 异步 | 通知 | 发布／订阅 |
|  | 请求／异步响应 | 发布／异步响应 |

同步调用：REST（JAX-RS、Spring Boot）、RPC（Thrift、Dubbo）

异步调用：Akka Actor、Kafka、Notify、MQ

### 数据如何管理？

<div align=center><img width="900" height="" src="./image/数据如何管理.png"/></div>

常见方式：共享数据库、消息队列事件驱动：Event Sourcing、CQRS

### 服务如何容错？

<div align=center><img width="900" height="" src="./image/服务如何容错.png"/></div>

防⽌应⽤用程序试图调⽤远程服务或访问共享资源失败

异常处理理、⽇日志记录、测试失败操作、资源分化、并发等等

### 服务如何监控？

<div align=center><img width="900" height="" src="./image/服务如何监控.png"/></div>
