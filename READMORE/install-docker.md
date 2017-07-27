## install docker

#### centos

   ```
   1.Remove old version of docker
    
     rpm -qa |grep docker
     yum  -y  remove docker* 
        
   2.install the new version of docker
    
     yum install -y docker-engine
        
   3.systemctl  start docker
    
   4.docker info check docker status
   ```

#### ubuntu

   ```
   1.update apt
    
     sudo apt-get update
        
   2.install docker
    
     sudo apt-get install docker-engine
        
   3.sudo service docker start
    
   4.docker info check docker status
   ```

#### mac

   see [https://docs.docker.com/docker-for-mac/](https://docs.docker.com/docker-for-mac/)


