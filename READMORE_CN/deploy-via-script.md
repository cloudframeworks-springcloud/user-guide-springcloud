## 通过脚本分别部署每个组件，命令如下

   ```
   docker run -d -p15672:15672 --name=rabbitmq rabbitmq:3-management

   docker run -d -e CONFIG_SERVICE_PASSWORD=${CONFIG_SERVICE_PASSWORD} -p 8888:8888 --name=config goodraincloudframeworks/piggymetrics-config
    
   docker run -d -e CONFIG_SERVICE_PASSWORD=${CONFIG_SERVICE_PASSWORD} --link config:config --name=registry -p 8761:8761 goodraincloudframeworks/piggymetrics-registry
    
   docker run -d -e MONGODB_PASSWORD=${MONGODB_PASSWORD} --name auth-mongodb goodraincloudframeworks/piggymetrics-mongodb
    
   docker run -d  -e CONFIG_SERVICE_PASSWORD=${CONFIG_SERVICE_PASSWORD} -e NOTIFICATION_SERVICE_PASSWORD=${NOTIFICATION_SERVICE_PASSWORD} -e STATISTICS_SERVICE_PASSWORD=${STATISTICS_SERVICE_PASSWORD} -e ACCOUNT_SERVICE_PASSWORD=${ACCOUNT_SERVICE_PASSWORD} -e MONGODB_PASSWORD=${MONGODB_PASSWORD} --link config:config --link auth-mongodb:auth-mongodb --link registry:registry --name=auth-service goodraincloudframeworks/piggymetrics-auth-service
    
   docker run -d -e MONGODB_PASSWORD=${MONGODB_PASSWORD} --name account-mongodb goodraincloudframeworks/piggymetrics-mongodb

   docker run -d -e CONFIG_SERVICE_PASSWORD=${CONFIG_SERVICE_PASSWORD} -e ACCOUNT_SERVICE_PASSWORD=${ACCOUNT_SERVICE_PASSWORD} -e MONGODB_PASSWORD=${MONGODB_PASSWORD} --link config:config --link account-mongodb:account-mongodb --link registry:registry --link auth-service:auth-service --link rabbitmq:rabbitmq --name=account-service goodraincloudframeworks/piggymetrics-account-service
    
   docker run -d -e MONGODB_PASSWORD=${MONGODB_PASSWORD} --name statistics-mongodb goodraincloudframeworks/piggymetrics-mongodb

   docker run -d -e CONFIG_SERVICE_PASSWORD=${CONFIG_SERVICE_PASSWORD} -e STATISTICS_SERVICE_PASSWORD=${STATISTICS_SERVICE_PASSWORD} -e MONGODB_PASSWORD=${MONGODB_PASSWORD} --link config:config --link statistics-mongodb:statistics-mongodb --link registry:registry --link auth-service:auth-service --link rabbitmq:rabbitmq --name=statistics-service goodraincloudframeworks/piggymetrics-statistics-service
    
   docker run -d -e MONGODB_PASSWORD=${MONGODB_PASSWORD} --name notification-mongodb goodraincloudframeworks/piggymetrics-mongodb
    
   docker run -d -e CONFIG_SERVICE_PASSWORD=${CONFIG_SERVICE_PASSWORD} -e NOTIFICATION_SERVICE_PASSWORD=${NOTIFICATION_SERVICE_PASSWORD} -e MONGODB_PASSWORD=${MONGODB_PASSWORD} --link config:config --link statistics-mongodb:statistics-mongodb --link registry:registry --link auth-service:auth-service --link rabbitmq:rabbitmq --name=notification-service goodraincloudframeworks/piggymetrics-notification-service
    
   docker run -ti -e CONFIG_SERVICE_PASSWORD=${CONFIG_SERVICE_PASSWORD} --link config:config --link registry:registry --link rabbitmq:rabbitmq --name=monitoring -p 9000:8080 -p 8989:8989 goodraincloudframeworks/piggymetrics-monitoring
    
   docker run -d -e CONFIG_SERVICE_PASSWORD=${CONFIG_SERVICE_PASSWORD} --link config:config --link registry:registry --link auth-service:auth-service --name=gateway -p 80:4000 goodraincloudframeworks/piggymetrics-gateway
   ```
