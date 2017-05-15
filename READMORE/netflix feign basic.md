## 进一步了解Netflix Feign

Feign是一个声明式、模板化的HTTP客户端，它使得写web服务变得更简单。使用Feign,只需要创建一个接口并注解。它具有可插拔的注解特性，包括Feign 注解和JAX-RS注解。Feign同时支持可插拔的编码器和解码器。当我们使用feign的时候，spring cloud 整和了Ribbon和Eureka去提供负载均衡。

简而言之：1）feign采用的是接口加注解；2）feign 整合了Ribbon。

#### 创建feign service

* 创建一个mvn工程，起名为feign,其pom.xml见实例代码，核心依赖如下：

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

* 在程序的入口Application类加上@EnableFeignClients注解开启配置服务器

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

* 创建一个远程掉用服务

   ```
   @FeignClient("eureka-service")
   public interface RemoteInvokerService {
        
       @RequestMapping(value = "/demo/show", method = RequestMethod.GET)
       public String remoteInvoker();
   }
   ```

   eureka-service： 是我们在eureka模块中注册的服务

   远程掉用/demo/show这个rest接口，也可以改成／demo/index 等

* 配置文件

   ```
   spring.application.name=feign
   server.port=5000
   eureka.client.serviceUrl.defaultZone=http://${EUREKA_HOST}:${EUREKA_PORT}/eureka/
   eureka.instance.preferIpAddress=true      
   ```
    
   EUREKA_HOST：注册中心ip

   EUREKA_PORT：注册中心端口

* 访问地址

   http://DOCKER_HOST:DOCKER_PORT/feign
