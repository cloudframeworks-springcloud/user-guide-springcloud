# Netflix Feign 使用向导

Spring Cloud集成Netflix Ribbon和Netflix Eureka提供的负载均衡的HTTP客户端Netflix Feign.

Netflix Feign是一个声明式、模板化的HTTP客户端，因此编写起来会更容易一些。Spring Cloud集成了Netflix Feign，并通过Netflix Ribbon和Netflix Eureka提供负载均衡。

使用Netflix Feign创建一个接口并对它进行注解（可插拔的注解支持，包括Feign注解），在应用主类中通过`@EnableFeignClients`注解开启Feign功能，并使用`@FeignClient`(服务ID)注解来绑定该接口对应服务。

## 如何创建一个Netflix Feign

代码参考：[https://github.com/cloudframeworks-springcloud/Spring-Cloud-Feign.git](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Feign.git)

**第一步：创建普通的应用**

**第二步：将该应用主类中加入`@EnableFeignClients`**

**第三步：在service中用@FeignClient(服务ID)注解来绑定该接口对应服务**

**第四步：修改配置文件(根据自己的环境设置EUREKA_HOST和EUREKA_PORT)**

`eureka.client.serviceUrl.defaultZone=http://127.0.0.1:5000/eureka/v2/`

**第五步：构建镜像，运行service**

### 完整代码

```
        git https://github.com/cloudframeworks-springcloud/Spring-Cloud-Feign.git
        
        cd  Spring-Cloud-Feign && docker build -t feign .
        
        docker run -d -p 5000:5000 feign
```

