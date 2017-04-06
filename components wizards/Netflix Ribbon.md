# Netflix Ribbon 使用向导

代码参考：[https://github.com/cloudframeworks-springcloud/Netflix-Ribbon.git](https://github.com/cloudframeworks-springcloud/Netflix-Ribbon.git)

1. 创建普通的应用

2. 将该应用主类中加入`@EnableFeignClients`

3. 在service中用`@FeignClient`(服务ID)注解来绑定该接口对应服务

4. 修改配置文件(根据自己的环境设置`EUREKA_HOST`和`EUREKA_PORT`) 

5. 构建镜像，运行service

**[完整代码]**

```
       git https://github.com/cloudframeworks-springcloud/Netflix-Ribbon.git
        
        cd  Netflix-Ribbon && docker build -t ribbon .
        
        docker run -ti -e "EUREKA_HOST=172.17.0.4" -e "EUREKA_PORT=8761" -p 5000:5000 ribbon
```
