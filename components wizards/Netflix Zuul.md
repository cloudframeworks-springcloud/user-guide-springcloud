# Netflix Zuul 使用向导

### 如何创建一个Netflix Zuul

代码参考：[https://github.com/cloudframeworks-springcloud/Netflix-Zuul.git](https://github.com/cloudframeworks-springcloud/Netflix-Zuul.git)

1. 创建普通的应用

2. 将该应用主类中加入`@EnableZuulProxy`

3. 修改配置文件(根据自己的环境设置`EUREKA_HOST`和`EUREKA_PORT`)

4. 构建镜像，运行service

**[完整代码]**

```
        git https://github.com/cloudframeworks-springcloud/Netflix-Zuul.git
        
        cd  Netflix-Zuul && docker build -t zuul .
        
        docker run -ti -e "EUREKA_HOST=172.17.0.4" -e "EUREKA_PORT=8761" -p 5000:5000 zuul
```
