## install docker

#### centos

   ```
   1.清除docker 旧版本
    
     rpm -qa |grep docker
     yum  -y  remove docker* 
        
   2.安装新的docker
    
     yum install -y docker-engine
        
   3.systemctl  start docker
    
   4.docker info 查看docker状态
   ```

#### ubuntu

   ```
   1.更新apt包
    
     sudo apt-get update
        
   2.安装 Docker
    
     sudo apt-get install docker-engine
        
   3.sudo service docker start
    
   4.docker info 查看docker状态
   ```

#### mac

   请参考[https://docs.docker.com/docker-for-mac/](https://docs.docker.com/docker-for-mac/)
