# spring cloud feign 使用向导

Feign 是一个声明web服务客户端，这便得编写web服务客户端更容易，使用Feign 创建一个接口并对它进行注解，它具有可插拔的注解支持包括Feign注解, Spring Cloud 集成 Ribbon 和 Eureka 提供的负载均衡的HTTP客户端 Feign.在应用主类中通过@EnableFeignClients注解开启Feign功能;使用@FeignClient(服务ID)注解来绑定该接口对应服务

# 如何创建一个feign

具体代码参加：https://github.com/cloudframeworks-springcloud/Spring-Cloud-Feign.git
第一步：创建普通的应用
第二步：将该应用主类中加入@EnableFeignClients
第三步：在service中用@FeignClient(服务ID)注解来绑定该接口对应服务
第四步：修改配置文件(根据自己的环境设置EUREKA_HOST和EUREKA_PORT) eureka.client.serviceUrl.defaultZone=http://127.0.0.1:5000/eureka/v2/
第五步：构建镜像，运行service

完整代码：

    <code>
        git https://github.com/cloudframeworks-springcloud/Spring-Cloud-Feign.git
        
        cd  Spring-Cloud-Feign && docker build -t feign .
        
        docker run -d -p 5000:5000 feign
    </code>



