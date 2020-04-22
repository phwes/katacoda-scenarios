## Update system
Katacoda's ubuntu image has not updated it's PPAs for a while. This might take a while:  
`apt update`{{execute}}  
To interact with our mysql container, when it has been started, we will use the normal mysql-client:  
`apt install mysql-client`{{execute}}  

# MySQL

## Downloading images
Docker is built around so called images...  
`docker pull mysql`{{execute}}   

## Create persistant storage, Volume
`mkdir /root/mysql_volume`{{execute}}

## Set up MySQL container
First we will start an MySQL container...  
`docker run --name m1 -v /root/mysql_volume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=guest -d mysql`{{execute}}
MySQL stores its data in /var/lib/mysql so therefore we connected the persistent storage to that directory.  
*Note: Katacoda can experience some frome time to time. Meaning that a command fails. Wait a moment and try the command again.*   
To access...  
`mysql -uroot -pguest -h 172.18.0.2 -P 3306`{{execute}}  
Try a command...  
`show databases;`{{execute}}  
## Fix hashing
The PHP version we will use and MySQL are experienceing some password compatability issues, unrelated to docker.  
To fix this, for the root user, we run the following command in the mysql tty:  
´ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'guest';´ {{execute}}  
