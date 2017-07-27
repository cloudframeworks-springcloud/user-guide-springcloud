## 进一步了解Netflix Hystrix

Netflix Hystrix是一个延迟和容错库，旨在隔离远程系统，服务和第三方库的访问点，停止级联故障，并在不可避免的故障的复杂分布式系统中启用弹性。

#### 创建Hystrix service

* 创建一个mvn工程，起名为hystrix-service，核心依赖如下：

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-netflix-hystrix-stream</artifactId>
   </dependency>       
   ```

* 在程序的入口Application

   ```
   @SpringBootApplication
   @EnableDiscoveryClient
   @EnableFeignClients
   public class HystrixDemoApplication {
        
       public static void main(String[] args) {
           SpringApplication.run(HystrixDemoApplication.class, args);
       }
   }   
   ```

* 创建一个远程调用服务

   ```
   @Service
   public class RemoteShowService {
        
       @Autowired
       private RestTemplate restTemplate;
        
       @HystrixCommand(fallbackMethod = "reliable", groupKey = "Demo", commandKey = "Show", commandProperties = { @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "1000") })
       public String remoteShow() {
           return restTemplate.getForObject("http://EUREKA-SERVICE/demo/show", String.class);
       }
    
       public String reliable() {
           return "fallback Method";
       }
   }
   ```

   @HystrixCommand： 自定义拦截机制
   
   EUREKA-SERVICE：在eureka模块中注册的服务
    
* 创建另一个远程调用服务

   ```
   @RestController
   @RequestMapping("/first")
   public class HystrixHelloController {
    
       @Autowired
       private RemoteInvokerService remoteInvokerService;
    
       @RequestMapping("hystrix")
       @HystrixCommand(fallbackMethod = "failme", groupKey = "Demo", commandKey = "first", commandProperties = { @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "10000") })
       public String remoteHello() {
           return remoteInvokerService.remoteInvoker();
       }
        
       protected String failme() {
           return "failed invoked Method";
       }
   }
   ```

   @HystrixCommand： 自定义拦截机制

   EUREKA-SERVICE：在eureka模块中注册的服务

* 配置文件

   ```
   spring.application.name=hystrix-service
   server.port=5000
   eureka.client.serviceUrl.defaultZone=http://${EUREKA_HOST}:${EUREKA_PORT}/eureka/
   eureka.instance.preferIpAddress=true    
   ```
    
   EUREKA_HOST：注册中心ip

   EUREKA_PORT：注册中心端口

* 访问地址

   http://DOCKER_HOST:DOCKER_PORT/first

   http://DOCKER_HOST:DOCKER_PORT/second

#### 创建Hystrix monitoring

* 创建一个mvn工程，起名为hystrix-monitoring，核心依赖：

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-turbine-stream</artifactId>
   </dependency>
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
   </dependency>
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-hystrix-dashboard</artifactId>
   </dependency>        
   ```

   基于rabbitmq去收集聚合

* 在程序的入口Application，加入@EnableTurbineStream 和 @EnableHystrixDashboard

   ```
   @@SpringBootApplication
   @EnableTurbineStream
   @EnableHystrixDashboard
   public class MonitoringApplication {
    
       public static void main(String[] args) {
           SpringApplication.run(MonitoringApplication.class, args);
       }
   }      
   ```

* 配置文件

   ```
   eureka:
     instance:
       prefer-ip-address: true
     client:
       serviceUrl:
         defaultZone: http://EUREKA_HOST:EUREKA_PORT/eureka/
    
   spring:
     application:
       name: hystrix-monitor
     rabbitmq:
       host: rabbitmq     
   ```

   EUREKA_HOST：注册中心ip

   EUREKA_PORT：注册中心端口

* 访问地址

   http://DOCKER_HOST:8080/hystrix 页面中加入 http://DOCKER_HOST:8989/
