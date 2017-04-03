# spring cloud eureka 使用向导

在微服务架构中，由于每一个服务的粒度相对传统SOA来说要小的多，所以服务的数量会成倍增加；有效的管理各个服务有为重要，这是就出现了服务注册的概念；服务注册的本质：
1、简单易用，对用户透明
2、高可用，满足cap理论
3、多语言支持

springcloud 中采用eureka做为注册中心，它也可以用zookeeper做注册中心，本文主要采用eureka做注册中心

Eureka的易用性体现在两方面，一是通过与Spring Boot(Cloud)结合达到了只用注解和maven依赖就能部署和启动服务的效果，二是Eureka自带Client包，使得使用Eureka作为注册中心的客户端（即服务）不需要关心自己与Eureka的通讯机制只需要引入Client依赖即可，当然前提是使用Java。

Eureka通过“伙伴”机制实现高可用。每一台Eureka都需要在配置中指定另一个Eureka的地址作为伙伴，Eureka启动时会向自己的伙伴节点获取当前已经存在的注册列表， 这样在向Eureka集群中新加机器时就不需要担心注册列表不完整的问题，在cap理论中满足ap原则。除此之外，Eureka还支持Region和Zone的概念。其中一个Region可以包含多个Zone。Eureka在启动时需要指定一个Zone名，即当前Eureka属于哪个zone, 如果不指定则属于defaultZone。Eureka Client也需要指定Zone。

Eureka是用Java编写的，但它会将所有注册信息和心跳连接地址都暴露为HTTP REST接口，客户端实际是通过HTTP请求与Server进行通讯的，因此，Client完全可以使用其它语言进行编写，只需要即时调用注册服务、注销服务、获取服务列表和心跳请求的HTTP REST接口即可


#如何搭建一个Eureka server

第一步：创建eureka server 参见：https://github.com/cloudframeworks-springcloud/Netflix-Eureka-server
第二步：运行eureka server
第三步：访问http://127.0.0.1:5000


#如何注册一个Eureka service

第一步：创建普通的应用服务
第二步：将该服务注册到eureka中（通过@EnableDiscoveryClient）参见：https://github.com/cloudframeworks-springcloud/Netflix-Eureka-service
第三步：运行eureka service
第四步：去eureka中查看是否已注册成功
备注：用户可以定义自己的业务逻辑


