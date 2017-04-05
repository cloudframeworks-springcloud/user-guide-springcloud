# Spring Cloud Config 使用向导

目前在项目中用到的配置切换方式经常是通过配置文件进行切换的，比如java语言开发的项目使用Maven定义profile进行，配置的修改需要重新打包，当部署节点大量增加，打包和部署就变成了一项大工程。现阶段流行的配置管理平台有disconf、diamond、qconf等。

Spring Cloud微服务套件也提供了配置管理组件Spring Cloud Config，基于使用中心配置仓库的思想（版本控制），支持Git、SVN。

## 如何搭建一个config server

**第一步：选择Git或SVN作为你的配置仓库**（这里选择git作为配置仓库）

**第二步：创建相应的配置文件**，如：[https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config.git](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config.git)

**第三步：创建Spring Cloud Config server**，参考：[https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server)

**第四步：创建Spring Cloud Config client，并从config server获取配置仓库中的信息**，参考：[https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client](https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client)

**第五步：运行`cloud-config server`和`cloud-config client`**
