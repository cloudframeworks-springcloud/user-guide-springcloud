# spring cloud config 使用向导

目前在项目中用到的配置切换方式经常是通过配置文件进行切换，比如java语言开发的项目使用maven定义profile进行的，配置的修改需要重新打包，部署节点一多，打包和部署就变成了一项大工程。先阶段流行的配置管理平台有disconf、diamond、qconf等。
今天我们介绍springcloud如何进行配置文件管理。SpringCloud微服务套件也提供了配置管理组件spring-cloud-config，基于使用中心配置仓库的思想（版本控制），支持git、svn

#如何搭建一个config server

第一步：选择git、svn作为你的配置仓库，我们选择git作为配置仓库
第二步：创建相应的配置文件如：https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config.git
第三步：创建springcloud config server 参见：https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-server
第四步：创建springcloud config client，从config server那里获取配置仓库中的信息，参见：https://github.com/cloudframeworks-springcloud/Spring-Cloud-Config-client
第五步：运行cloud-config server 和 cloud-config client


