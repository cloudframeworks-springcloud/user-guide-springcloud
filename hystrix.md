# spring cloud hystrix 使用向导


# 如何创建一个hystrix

具体代码参加：https://github.com/cloudframeworks-springcloud/Netflix-Hystrix.git
第一步：创建普通的应用
第二步：将该应用主类中加入@EnableFeignClients
第三步：在service中用@HystrixCommand来设置熔断
第四步：修改配置文件(根据自己的环境设置EUREKA_HOST和EUREKA_PORT) eureka.client.serviceUrl.defaultZone=http://127.0.0.1:5000/eureka/v2/
第五步：构建镜像，运行service

完整代码：

    <code>
        git https://github.com/cloudframeworks-springcloud/Netflix-Hystrix.git
        
        cd  Netflix-Hystrix && docker build -t hystrix .
        
        docker run -d -p 5000:5000 hystrix
    </code>



