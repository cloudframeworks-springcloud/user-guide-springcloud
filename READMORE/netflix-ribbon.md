## Read more about Netflix Ribbon

Ribbon是一个客户端负载均衡器，有多种负载均衡策略可选（包括自定义的负载均衡算法），并可配合服务发现及断路器使用。在配置文件中列出Load Balancer后面所有的机器，Ribbon会自动的帮助你基于某种规则（如简单轮询、随机连接等）去连接这些机器。

Ribbon的主要特点包括：1）负载均衡，2）容错，3）在异步和反应模型中支持多协议（HTT、TCP、UDP），4）缓存和批处理

Ribbon is a client load balancing with variety of load balancing strategies, can be used with service discovery and circuit breakers. Lists all the machines in the configuration, and Ribbon will automatically connect those machines based on certain rules (simple polling, random connections, etc.)

Ribbon can do 1) load balancing; 2) fault-tolerance; 3) support multi-protocol (HTT, TCP, UDP) in asynchronous and reactive models; 4) cache and batch

#### Build Ribbon service

* Build mvn and name it ribbon, core dependencies:

   ```
    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-ribbon</artifactId>
   </dependency>     
   ```

* In the application class of application entry

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
    
   @LoadBalanced: declare a loadBalanced template
   
* Create a remote call service

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

   EUREKA-SERVICE is the service registered in eureka module
   
   remote call /demo/show REST interface, can be replace with ／demo/index etc.

* Configuration

   ``` 
   spring.application.name=ribbon
   server.port=5000
   eureka.client.serviceUrl.defaultZone=http://${EUREKA_HOST}:${EUREKA_PORT}/eureka/
   eureka.instance.preferIpAddress=true     
   ```
    
   EUREKA_HOST: registry ip

   EUREKA_PORT: registry interface

* Address

    http://DOCKER_HOST:DOCKER_PORT/ribbon


