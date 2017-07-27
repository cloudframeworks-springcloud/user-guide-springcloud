## Read more about Netflix Hystrix

Netflix Hystrix is a latency and fault-tolerant library designed to isolate access points from remote systems, services and third-party libraries, stop cascading failures, and enable resiliency in complex, distributed systems with unavoidable failures.

#### Build Hystrix service

* Build mvn and name it hystrix-service, core dependencies:

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-netflix-hystrix-stream</artifactId>
   </dependency>       
   ```

* In the application class of application entry

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

* Create a remote call service

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

   @HystrixCommand： custom blocking mechanism
   
   EUREKA-SERVICE is the service registered in the eureka module
    
* Create another remote call service

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

   @HystrixCommand: custom blocking mechanism

   EUREKA-SERVICEis the service registered in the eureka module

* Configuration

   ```
   spring.application.name=hystrix-service
   server.port=5000
   eureka.client.serviceUrl.defaultZone=http://${EUREKA_HOST}:${EUREKA_PORT}/eureka/
   eureka.instance.preferIpAddress=true    
   ```
    
   EUREKA_HOST：registry ip

   EUREKA_PORT：registry interface

* Address

   http://DOCKER_HOST:DOCKER_PORT/first

   http://DOCKER_HOST:DOCKER_PORT/second

#### Build Hystrix monitoring

* Build mvn and name it hystrix-monitoring, core denpendencies:

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

   Collection based on Rabbitmq

* Add @EnableTurbineStream and @EnableHystrixDashboard in the Application class of application entry

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

* Configuration

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

   EUREKA_HOST: registry ip

   EUREKA_PORT: registry interface

* Address

   add http://DOCKER_HOST:8989/ in http://DOCKER_HOST:8080/hystrix


