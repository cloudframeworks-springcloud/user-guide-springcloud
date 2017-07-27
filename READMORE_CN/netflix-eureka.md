## 进一步了解Netflix Eureka

微服务架构比传统SOA架构中的服务粒度更小、服务数量更多，为了有效管理各个服务，服务注册的概念应运而生。它的特点是1）简单易用，对用户透明；2）高可用，满足CAP理论；3）多语言支持。

在基于Spring Cloud的微服务架构中，通常采用Netflix Eureka作为注册中心，它的易用性体现在：

* 通过与Spring Boot(Cloud)结合达到只用注解和Maven依赖即可部署和启动服务的效果
* Netflix Eureka自带Client包，使得使用Eureka作为注册中心的客户端（即服务）不需要关心自己与Eureka的通讯机制，只需要引入Client依赖即可，当然前提是使用Java

Netflix Eureka通过“伙伴”机制实现高可用，每一台Eureka都需要在配置中指定另一个Eureka的地址作为伙伴，Eureka启动时会向自己的伙伴节点获取当前已经存在的注册列表，这样在向Eureka集群中增加新机器时就不需要担心注册列表不完整的问题，在CAP理论中满足AP原则。

除此之外，Netflix Eureka支持Region和Zone的概念，其中一个Region可以包含多个Zone。Eureka在启动时需要指定一个Zone名，即指定当前Eureka属于哪个Zone, 如果不指定则属于defaultZone。值得注意的是，Eureka Client也需要指定Zone。

Netflix Eureka使用Java编写，但它会将所有注册信息和心跳连接地址都暴露为HTTP REST接口，客户端实际是通过HTTP请求与Server进行通讯的，因此Client完全可以使用其它语言进行编写，只需要即时调用注册服务、注销服务、获取服务列表和心跳请求的HTTP REST接口即可。

#### 创建Eureka Server

* 创建一个mvn工程，起名为eureka-server，核心依赖：

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-eureka-server</artifactId>
   </dependency>
        
   ```

* 在程序的入口Application类加上@EnableEurekaServer注解开启配置服务器

   ```
   @SpringBootApplication
   @EnableEurekaServer
   public class EurekaApplication {
    
       public static void main(String[] args) {
           SpringApplication.run(EurekaApplication.class, args);
       }
   }
        
   ```

* 配置文件

   ```    
   server:
     port: 8761
   spring:
     application:
       name: eureka-server
   eureka:
     instance:
       prefer-ip-address: true
     client:
       registerWithEureka: false
       fetchRegistry: false
       serviceUrl:
         defaultZone: http://127.0.0.1:8761/eureka/
       server:
         waitTimeInMsWhenSyncEmpty: 0
     server
       eviction-interval-timer-in-ms: 4000
       enableSelfPreservation: false
       renewalPercentThreshold: 0.9       
   ```

#### 创建Eureka service

* 创建一个mvn工程，起名为eureka-service，核心依赖：

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-eureka</artifactId>
   </dependency>
   ```

* 在程序的入口Application类加上@EnableDiscoveryClient注解开启配置服务器

   ```
   @SpringBootApplication
   @EnableDiscoveryClient
   public class DemoServiceApplication {
    
       public static void main(String[] args) {
           SpringApplication.run(DemoServiceApplication.class, args);
       }
   }     
   ```

* 创建2个restful接口

   普通的demo程序，提供/demo/show 和 /demo/index 接口
    
   ```
   @RequestMapping("/demo")
   @RestController
   public class DemoController {
    
       @RequestMapping("/show")
       public String show() {
           return "demo show";
       }
        
       @RequestMapping("/index")
       public String index() {
           return "demo index";
       }
   }
   ```
    
   user程序，提供/user/online和/user/offline 接口, 其中EurekaDiscoveryClientConfiguration管理改服务在注册中心的声明周期(下线和上线)
    
   ```
   @RequestMapping("/user")
   @RestController
   public class UserController {
       @Autowired
       private EurekaDiscoveryClientConfiguration lifecycle;
    
       @RequestMapping("/online")
       public String online() {
           this.lifecycle.start();
           return "user online method";
       }
    
       @RequestMapping("/offline")
       public String offline() {
           this.lifecycle.stop();
           return "user offline method";
       }
   }    
   ```

* 配置文件

   ```
   spring.application.name=eureka-service
   server.port=5000
   eureka.region=default
   eureka.preferSameZone=false
   eureka.shouldUseDns=false
   eureka.client.serviceUrl.defaultZone=http://${EUREKA_HOST}:${EUREKA_PORT}/eureka/
   eureka.instance.preferIpAddress=true
   eureka.instance.leaseRenewalIntervalInSeconds=10
   eureka.instance.leaseExpirationDurationInSeconds=20       
   ```
    
   EUREKA_HOST：注册中心ip
   
   EUREKA_PORT：注册中心端口
    
* 访问地址

   http://DOCKER_HOST:DOCKER_PORT/demo/index
       
   http://DOCKER_HOST:DOCKER_PORT/demo/show
       
   http://DOCKER_HOST:DOCKER_PORT/user/online
       
   http://DOCKER_HOST:DOCKER_PORT/user/offline
   
* 访问注册中心可以看到eureka-service已注册

   http://EUREKA_HOST:EUREKA_PORT/eureka/
