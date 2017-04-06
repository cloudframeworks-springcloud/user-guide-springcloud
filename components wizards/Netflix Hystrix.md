# Netflix Hystrix 使用向导

代码参考：[https://github.com/cloudframeworks-springcloud/Netflix-Hystrix](https://github.com/cloudframeworks-springcloud/Netflix-Hystrix.git)

1. 创建普通的应用

2. 将该应用主类中加入`@EnableFeignClients`

3. 在service中用`@HystrixCommand`来设置熔断

4. 修改配置文件(根据自己的环境设置EUREKA_HOST和EUREKA_PORT)

5. 构建镜像，运行service

**[完整代码]**

```
        git https://github.com/cloudframeworks-springcloud/Netflix-Hystrix.git
        
        cd  Netflix-Hystrix && docker build -t hystrix .
        
        docker run -ti -e "EUREKA_HOST=172.17.0.4" -e "EUREKA_PORT=8761" -p 5000:5000 hystrix
```
