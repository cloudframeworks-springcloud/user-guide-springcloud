## Read more about Netflix Ribbon

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


