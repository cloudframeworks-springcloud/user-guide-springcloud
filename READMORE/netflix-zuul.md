## Read more about Netflix Zuul

Netflix Zuul provides edge services for dynamic routing, monitoring, resiliency, and security.

Netflix Zuul provides front-door protection for microservice providers in a microservice architecture that provides REST APIs through a unified service gateway, while migrating rights to these heavier non-business logic content to the service routing layer Clusters can have higher reusability and testability.

#### Build Zuul service

* Build mvn and name it zuul, core dependencies:

   ```
    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-zuul</artifactId>
   </dependency>       
   ```

* Start the configuration server by adding @EnableZuulProxy in the Application class of application entry

   ``` 
   @SpringBootApplication
   @EnableDiscoveryClient
   @EnableZuulProxy
   public class GatewayApplication {
    
       public static void main(String[] args) {
           SpringApplication.run(GatewayApplication.class, args);
       }
   }     
   ```

* Configuration

   ``` 
   server:
     port: 5000
    
   spring:
     application:
       name: zuul
    
   eureka:
     client:
       service-url:
         defaultZone: http://${EUREKA_HOST}:${EUREKA_PORT}/eureka/
    
   hystrix:
     command:
       default:
         execution:
           isolation:
             thread:
               timeoutInMilliseconds: 20000
    
   ribbon:
     ReadTimeout: 20000
     ConnectTimeout: 20000
    
   zuul:
     ignoredServices: '*'
     host:
       connect-timeout-millis: 20000
       socket-timeout-millis: 20000
    
     routes:
       routes:
       demo:
         path: /demo/**
         serviceId: eureka-service
         stripPrefix: false
         sensitiveHeaders: Cookie,Set-Cookie,Authorization
       user:
         path: /user/**
         serviceId: eureka-service
         stripPrefix: false
         sensitiveHeaders: Cookie,Set-Cookie,Authorization
       outer:
         path: /baidu/**
         url: http://www.baidu.com
   ```
    
   EUREKA_HOST: registry ip
   
   EUREKA_PORT: registry interface
    
* Address

   http://DOCKER_HOST:DOCKER_PORT/feign


