## Read more about Netflix Eureka

Service granularity of microservice architecture is smaller than SOA architecture, and the amount of services is bigger, then the concept of service registration has merged. The service registration of microservice architecture is 1) easy to use, transparent to users; 2) high availability, to meet the CAP theory; 3) support multi-language.

Microservice architecture with Spring Cloud usually use Netflix Eureka as its registry, and its ease of use is reflected in:

* combine with Spring Boot to achieve the effect of deploying and launching services with annotations and Maven dependencies only
* Netflix Eureka comes with the Client package that we don't need to consider the communication mechanism with Eureka

Netflix is highly available through the "partner" mechanism, each Eureka need to specify another Eureka address as a partner in the configuration. Eureka will get the current registration list from its partner node, and when adding new machines in Eureka cluster, we don't need worry about the incomplete of registration list, that is, the AP principle is satisfied in the CAP theory.

In addition, Netflix Eureka supports the concept of Region and Zone, and a Region can contains multiple zones. Eureka need to specify a Zone name when launching, this indicate the Eureka belongs to which Zone (defaultZone if not specified). We also need to specify a Zone to Eureka Client.

Netflix Eureka is written in JAVA, but it exposes all registration and heartbeat connections to HTTP REST interface. The Client communicates with Server by HTTP request, which means Client can be written with any other language, just let the Client call registration service, logout service, get the service list and heartbeat request HTTP REST interface in real time.

#### Build Eureka Server

* Build mvn and name it eureka-server, core dependencies：

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-eureka-server</artifactId>
   </dependency>
        
   ```

* Start the configuration server by adding @EnableEurekaServer in the Application class of application entry

   ```
   @SpringBootApplication
   @EnableEurekaServer
   public class EurekaApplication {
    
       public static void main(String[] args) {
           SpringApplication.run(EurekaApplication.class, args);
       }
   }
        
   ```

* Configuration

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

#### Build Eureka service

* Build mvn and name it eureka-service, core dependencies:

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-eureka</artifactId>
   </dependency>
   ```

* Start the configuration server by adding @EnableDiscoveryClient in the Application class of application entry

   ```
   @SpringBootApplication
   @EnableDiscoveryClient
   public class DemoServiceApplication {
    
       public static void main(String[] args) {
           SpringApplication.run(DemoServiceApplication.class, args);
       }
   }     
   ```

* Create 2 restful interfaces

   normal demo application with /demo/show and /demo/index interfaces
    
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
    
   user application with /user/online and /user/offline interfaces, EurekaDiscoveryClientConfiguration manage the service in registry's declaration cycle (offline and online)
    
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

* Configuration

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
    
   EUREKA_HOST：registry ip
   
   EUREKA_PORT：registry interface
    
* Address

   http://DOCKER_HOST:DOCKER_PORT/demo/index
       
   http://DOCKER_HOST:DOCKER_PORT/demo/show
       
   http://DOCKER_HOST:DOCKER_PORT/user/online
       
   http://DOCKER_HOST:DOCKER_PORT/user/offline
   
* Access registry, and we can see eureka-service had been registered

   http://EUREKA_HOST:EUREKA_PORT/eureka/


