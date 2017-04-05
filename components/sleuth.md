# spring cloud sleuth 使用向导

# 如何创建一个sleuth

具体代码参加：https://github.com/cloudframeworks-springcloud/Netflix-Ribbon.git
第一步：创建普通的应用
第二步：将该应用主类中加入@EnableFeignClients
第三步：在service中用@FeignClient(服务ID)注解来绑定该接口对应服务
第四步：修改配置文件(根据自己的环境设置EUREKA_HOST和EUREKA_PORT) eureka.client.serviceUrl.defaultZone=http://127.0.0.1:5000/eureka/
第五步：构建镜像，运行service

完整代码：

    <code>
        git https://github.com/cloudframeworks-springcloud/Spring-Cloud-Sleuth.git
        
        cd  Spring-Cloud-Sleuth && docker build -t sleuth .
        
        docker run -d -p 5000:5000 sleuth
    </code>



