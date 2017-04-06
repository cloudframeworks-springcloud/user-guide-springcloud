# Spring Cloud Config 使用向导

Spring Cloud Config提供解决分布式系统的配置管理方案，分server、client两个模块：

* config_server 配置服务器：统一配置系统中需要的各种服务
* config_client 配置客户端：根据Spring框架的Environment和PropertySource从spring cloud config sever获取各种配置

Spring Cloud Config基于使用中心配置仓库的思想（版本控制），支持Git（默认）、SVN、File等三种储存方式。

### 如何搭建Spring Cloud config

1. 选择Git或SVN作为你的配置仓库（这里选择git作为配置仓库）

2. 创建相应的配置文件，如：[https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config.git](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config.git)

3. 创建Spring Cloud Config server，参考：[https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server.git](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server.git)

4. 创建Spring Cloud Config client，并从config server获取配置仓库中的信息，参考：[https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client.git](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client.git)

5. 运行cloud-config server和cloud-config client

6. 访问 http://127.0.0.1:6000/from

**[完整代码]**

```
        git clone https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server.git
        
        cd  Spring-Cloud-Config-server && docker build -t config-server .
        
        docker run -d -p 5000:5000 config-server

        git clone https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client.git
        
        cd Spring-Cloud-Config-client && docker build -t config-client .
        
        docker run -ti -p 6000:5000 -e "CONFIG_HOST=172.17.0.2" -e "CONFIG_PORT=5000" config-client
        
```
