## Read more about Spring Cloud Config

In a distributed system, Spring Cloud Config provides extensible configuration services through config-server and config-client, and uses the configuration service center to centrally manage the various environment profiles for all services. Spring Cloud Config supports three ways of storing Git (default), SVN, and File, based on the idea of using the central repository (version control).

#### Build Config Server

* Build mvn and name it config-server, core dependencies:

   ```
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-test</artifactId>
       <scope>test</scope>
   </dependency>
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-config-server</artifactId>
    </dependency> 
   ```

* Start the configuration server by adding @EnableConfigServer in the Application class of application entry

   ```
   @EnableConfigServer
   @SpringBootApplication
   public class Application {
    
       public static void main(String[] args) {
           new SpringApplicationBuilder(Application.class).web(true).run(args);
       }
   }       
   ```

* Configuration

   ```
   server:
     port: 8888
    
   spring:
     application:
       name: config-server
     cloud:
       config:
         server:
           git:
             uri:                        ## The git address stored in the configuration file
             searchPaths: config         
        
   ```

   Obtaining resource information on git follows the following rules:

   ```
   /{application}/{profile}[/{label}]
   /{application}-{profile}.yml
   /{label}/{application}-{profile}.yml
   /{application}-{profile}.properties
   /{label}/{application}-{profile}.properties  
   ```

#### Build Config client

* Build mvn and name it config-client, core dependencies:

   ```
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-config-client</artifactId>
   </dependency>
   ```

* Start the configuration server by adding @EnableConfigServer in the Application class of application entry

   ```
   @SpringBootApplication
   public class Application {
    
       public static void main(String[] args) {
           new SpringApplicationBuilder(Application.class).web(true).run(args);
       }
   }        
   ```

* Create a restful interface to access configuration

   ```
   @EnableAutoConfiguration
   @RefreshScope
   @RestController
   public class DemoController {
    
       @Value("${from}")
       String from;
        
        
       @RequestMapping("/from")
       public String from() {
           return this.from;
       }
   }
   ```

* Configuration

   ```
   server:
     port: 9000
    
   spring:
     application:
       name: config-client
     profiles:
       active: dev
     cloud:
       config:
         uri: http://${CONFIG_HOST}:${CONFIG_PORT}
         label: master      
   ```

* Address

   http://DOCKER_HOST:DOCKER_PORT/from


