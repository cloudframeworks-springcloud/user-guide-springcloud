# Netflix Eureka 使用向导

相比传统SOA架构，微服务架构中的服务粒度更小、服务数量更多，如何有效管理各个服务就显得尤为重要，也因此出现了服务注册的概念。

服务注册的本质：1）简单易用，对用户透明；2）高可用，满足CAP理论；3）多语言支持

在基于Spring Cloud的微服务架构中，通常采用Netflix Eureka作为注册中心，某些情况下也会采用Zookeeper作为替代。

Netflix Eureka的易用性体现在两方面：

* 通过与Spring Boot(Cloud)结合达到只用注解和Maven依赖即可部署和启动服务的效果
* Netflix Eureka自带Client包，使得使用Eureka作为注册中心的客户端（即服务）不需要关心自己与Eureka的通讯机制，只需要引入Client依赖即可，当然前提是使用Java

**Netflix Eureka通过“伙伴”机制实现高可用**，每一台Eureka都需要在配置中指定另一个Eureka的地址作为伙伴，Eureka启动时会向自己的伙伴节点获取当前已经存在的注册列表，这样在向Eureka集群中增加新机器时就不需要担心注册列表不完整的问题，在CAP理论中满足AP原则。

除此之外，**Netflix Eureka支持Region和Zone的概念**，其中一个Region可以包含多个Zone。Eureka在启动时需要指定一个Zone名，即指定当前Eureka属于哪个Zone, 如果不指定则属于defaultZone。值得注意的是，Eureka Client也需要指定Zone。

Netflix Eureka使用Java编写，但它会将所有注册信息和心跳连接地址都暴露为HTTP REST接口，客户端实际是通过HTTP请求与Server进行通讯的，因此Client完全可以使用其它语言进行编写，只需要即时调用注册服务、注销服务、获取服务列表和心跳请求的HTTP REST接口即可。

### 如何搭建Netflix Eureka server

1. 下载Netflix Eureka server

Git地址：[https://github.com/cloudframeworks-springcloud/Netflix-Eureka-server.git](https://github.com/cloudframeworks-springcloud/Netflix-Eureka-server.git)

命令：`Git clone` [https://github.com/cloudframeworks-springcloud/Netflix-Eureka-server.git](https://github.com/cloudframeworks-springcloud/Netflix-Eureka-server.git)

2. 构建Netflix Eureka server镜像

命令：`cd  Netflix-Eureka-server && docker build -t eureka-server .`

3. 运行Netflix Eureka server

命令：`docker run -d -p 8761:8761 eureka-server`

4. 访问[http://127.0.0.1:8761](http://127.0.0.1:8761)

**[完整代码]**

```
        git clone https://github.com/cloudframeworks-springcloud/Netflix-Eureka-server.git
        
        cd  Netflix-Eureka-server && docker build -t eureka-server .
        
        docker run -d -p 8761:8761 eureka-server
```

### 注册一个服务到Eureka server

1. 创建普通的应用服务

2. 将该服务注册到Netflix Eureka中（通过`@EnableDiscoveryClient`）

3. 设置Eureka server的地址

修改配置文件(根据自己的环境设置`EUREKA_HOST`和`EUREKA_PORT`)
`eureka.client.serviceUrl.defaultZone=http://127.0.0.1:5000/eureka/v2/`

4. 运行Netflix Eureka service

5. 去Netflix Eureka中查看是否已注册成功(备注：用户可以定义自己的业务逻辑)

代码参考：[https://github.com/cloudframeworks-springcloud/Netflix-Eureka-service.git](https://github.com/cloudframeworks-springcloud/Netflix-Eureka-service.git)

**[完整代码]**

```
        git https://github.com/cloudframeworks-springcloud/Netflix-Eureka-service.git
        
        cd  Netflix-Eureka-service && docker build -t eureka-service .
        
        docker run -ti -e "EUREKA_HOST=172.17.0.4" -e "EUREKA_PORT=8761" -p 5000:5000 eureka-service
```
