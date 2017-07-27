## 进一步了解Netflix Ribbon

Ribbon是一个客户端负载均衡器，有多种负载均衡策略可选（包括自定义的负载均衡算法），并可配合服务发现及断路器使用。在配置文件中列出Load Balancer后面所有的机器，Ribbon会自动的帮助你基于某种规则（如简单轮询、随机连接等）去连接这些机器。

Ribbon的主要特点包括：1）负载均衡，2）容错，3）在异步和反应模型中支持多协议（HTT、TCP、UDP），4）缓存和批处理

#### 创建Ribbon service

* 创建一个mvn工程，起名为ribbon，核心依赖如下：

   ```
    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-ribbon</artifactId>
   </dependency>     
   ```

* 程序的入口Application类

   ``` 
   @SpringBootApplication
   @EnableDiscoveryClient
   public class RibbonApplication {
        
       @Bean
       @LoadBalanced
       RestTemplate restTemplate() {
           return new RestTemplate();
       }
    
       public static void main(String[] args) {
           SpringApplication.run(RibbonApplication.class, args);
       }
   }     
   ```
    
   @LoadBalanced：声明一个loadBalanced模版

* 创建一个远程调用服务

   ```
   @RestController
   public class DemoController {
    
       @Autowired
       RestTemplate restTemplate;
    
       @RequestMapping(value = "/ribbon", method = RequestMethod.GET)
       public String add() {
           return restTemplate.getForEntity("http://EUREKA-SERVICE/demo/show", String.class).getBody();
       }
   }
   ```

   EUREKA-SERVICE： 在eureka模块中注册的服务
    
   远程调用/demo/show这个rest接口，也可以改成／demo/index 等

* 配置文件

   ``` 
   spring.application.name=ribbon
   server.port=5000
   eureka.client.serviceUrl.defaultZone=http://${EUREKA_HOST}:${EUREKA_PORT}/eureka/
   eureka.instance.preferIpAddress=true     
   ```
    
   EUREKA_HOST：注册中心ip

   EUREKA_PORT：注册中心端口

* 访问地址

    http://DOCKER_HOST:DOCKER_PORT/ribbon
