## Update system
Katacoda's ubuntu image has not updated it's PPAs for a while. This might take a while:
`apt update`{{execute}}
To interact with our mysql container, when it has been started, we will use the normal mysql-client:
`install mysql-client`{{execute}}

## Downloading images
Docker is built around so called images...

`docker pull mysql`{{execute}}
`docker pull httpd`{{execute}}

## Set up MySQL container
First we will start an MySQL container...
`docker run --name m1 --ip 172.18.0.3 -e MYSQL_ROOT_PASSWORD=guest -d mysql`{{execute}}
To access...
`mysql -uroot -pguest -h 172.18.0.3 -P 3306`{{execute}}
Try a command...
`show databases;`{{execute}}
