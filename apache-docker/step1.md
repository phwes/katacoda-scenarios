## Update system
Katacoda's ubuntu image has not updated it's PPAs for a while. This might take a while:  
`apt update`{{execute}}  
To interact with our mysql container, when it has been started, we will use the normal mysql-client:  
`apt install mysql-client`{{execute}}  

# MySQL

## Downloading images
Docker containers are built from so called images. These images can either be built from a dockerfile, or loaded from the docker hub. If you try to run a container with a image that has not been downloaded, docker will search and pull the image from docker hub automatically. But for the sake of this tutorial, we will pull the MySQL image manually:     
`docker pull mysql:8.0.19`{{execute}}  
The nymbers after the colon refer to the version number. 

## Start a MySQL container
To create and start a docker container we use the `docker run [container image]` command. But we want to add a few parameters, so the container can match our needs:  
* *-v or --mount*, containers are stateless by design. This means that the are unable to store data when they are stopped or restarted. To counter this we can use either volumes or mount binds. Volumes and mounts will map a directory on the host machine to a directory in the container. This way data can be stored and loaded on the host machine even when the container has been stopped.  
* *--name*, docker will assign a name to the container if this parameter is not specified. But it is a nice feature to name your own containers.
* *-d*, this will simply daemonize the container so it won't block your shell.  
* *-e*, this sets environment variabels. We will use this to set the root password.

## Set up MySQL container
First we will start an MySQL container, MySQL stores its data in /var/lib/mysql so therefore we connect the persistent storage to that directory.  
`docker run --name m1 -v /root/mysql_volume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=guest -d mysql:8.0.19`{{execute}}  
Note that with the `-v` parameter, the mysql_volume is created automatically.  

## Test the MySQL database
*Note: Katacoda can experience some lag from time to time. Meaning that if a command fails, wait a moment and then try the command again.*   
To access...  
`mysql -uroot -pguest -h 172.18.0.2 -P 3306`{{execute}}  
Try a command...  
`show databases;`{{execute}}  
## Fix hashing
The PHP version we will use and MySQL are experienceing some password compatability issues, unrelated to docker.  
To fix this, for the root user, we run the following command in the mysql tty:  
`ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'guest';`{{execute}}  
