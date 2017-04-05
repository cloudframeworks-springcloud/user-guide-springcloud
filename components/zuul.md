# spring cloud zuul 使用向导

# 如何创建一个zuul

具体代码参加：https://github.com/cloudframeworks-springcloud/Netflix-Zuul.git
第一步：创建普通的应用
第二步：将该应用主类中加入@EnableZuulProxy
第三步：修改配置文件(根据自己的环境设置EUREKA_HOST和EUREKA_PORT) eureka.client.serviceUrl.defaultZone=http://127.0.0.1:5000/eureka/
第四步：构建镜像，运行service

完整代码：

    <code>
        git https://github.com/cloudframeworks-springcloud/Netflix-Zuul.git
        
        cd  Netflix-Zuul && docker build -t zuul .
        
        docker run -d -p 5000:5000 zuul
    </code>



