## Read more about Netflix Feign

Feign is a declarative, templated HTTP client that makes building web service easier. We can use Feign by create a interface and annotate it. Feign supports pluggable annotation, includes Feign annotate and JAX-RS annotate. Feign support pluggable encoders and decoders. When we use Feign, Spring Cloud integrated Ribbon and Eureka to provide load balancing.

In short: 1) Feign is using interface annotation; 2) Feign is integrated with Ribbon 

#### Build Feign service

* Build mvn and name it feign (check pom.xml in example code), core dependencies:

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-ribbon</artifactId>
   </dependency>
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-feign</artifactId>
   </dependency>       
   ```

* Start the configuration server by adding @EnableFeignServer in the Application class of application entry

   ```
   @SpringBootApplication
   @EnableDiscoveryClient
   @EnableFeignClients
   public class FeignDemoApplication {
        
       public static void main(String[] args) {
           SpringApplication.run(FeignDemoApplication.class, args);
       }
   }     
   ```

* Create a remote call service

   ```
   @FeignClient("eureka-service")
   public interface RemoteInvokerService {
        
       @RequestMapping(value = "/demo/show", method = RequestMethod.GET)
       public String remoteInvoker();
   }
   ```

   eureka-service is the service that we register in the eureka module

   remote call /demo/show REST interface, can replace it with ／demo/index etc.

* Configuration

   ```
   spring.application.name=feign
   server.port=5000
   eureka.client.serviceUrl.defaultZone=http://${EUREKA_HOST}:${EUREKA_PORT}/eureka/
   eureka.instance.preferIpAddress=true      
   ```
    
   EUREKA_HOST：registry ip

   EUREKA_PORT：registry interface

* Address

   http://DOCKER_HOST:DOCKER_PORT/feign


