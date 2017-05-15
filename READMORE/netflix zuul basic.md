## 进一步了解Netflix Zuul

Netflix Zuul提供动态路由、监控、弹性、安全等的边缘服务。

在通过服务网关统一向外的提供REST API的微服务架构中，Netflix Zuul为微服务机构提供了前门保护的作用，同时将权限控制这些较重的非业务逻辑内容迁移到服务路由层面，使得服务集群主体能够具备更高的可复用性和可测试性。

#### 创建zuul service

* 创建一个mvn工程，起名为zuul，核心依赖：

   ```
    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-zuul</artifactId>
   </dependency>       
   ```

* 在程序的入口Application类加上@EnableZuulProxy注解开启配置服务器

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

* 配置文件

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
    
   EUREKA_HOST：注册中心ip
   
   EUREKA_PORT：注册中心端口
    
* 访问地址

   http://DOCKER_HOST:DOCKER_PORT/feign
