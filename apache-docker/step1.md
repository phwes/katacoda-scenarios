## Update system
Katacoda's ubuntu image has not updated it's PPAs for a while. This might take a while:  
`apt update`{{execute}}  
To interact with our mysql container, when it has been started, we will use the normal mysql-client:  
`apt install mysql-client`{{execute}}  

# MySQL

## Downloading images
Docker containers are run from so called images. These images can either be built from a dockerfile, or loaded from the docker hub. If you try to run a container with an image that has not been downloaded, docker will search and pull the image from docker hub automatically. But for the sake of this tutorial, we will pull the MySQL image manually:     
`docker pull mysql:8.0.19`{{execute}}  
The numbers after the colon refer to the version number. 

## Start a MySQL container
To create and start a docker container we use the `docker run [container image]` command. But we want to add a few parameters, so the container can match our needs:  
* `-v` or `--mount`, containers are stateless by design. This means that the are unable to store data when they are stopped or restarted. To counter this we can use either volumes or mount binds. Volumes and mounts will map a directory on the host machine to a directory in the container. In this way data can be stored and loaded on the host machine even when the container has been stopped.  
* `--name`, docker will assign a name to the container if this parameter is not specified. But it is a nice feature to name your own containers.
* `-d`, this will simply daemonize the container so it won't block your shell.  
* `-e`, this sets environment variabels. We will use this to set the root password.

## Set up MySQL container
First we will start an MySQL container. MySQL stores its data in /var/lib/mysql so therefore we connect the persistent storage to that directory.  
`docker run --name m1 -v /root/mysql_volume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=guest -d mysql:8.0.19`{{execute}}  
Note that with the `-v` parameter, the directory mysql_volume is created automatically.  

## Test the MySQL database
*Note: Katacoda can experience some lag from time to time. Meaning that if a command fails, wait a moment and then try the command again.*   
To access the MySQL databases inside the container we simply run the `mysql` command from our host. This will connect to the MySQL interface on port 3306 on the container.  
`mysql -uroot -pguest -h 172.18.0.2 -P 3306`{{execute}}  
Since this is the first container we assume it starts on the IP 172.18.0.2, but if this was incorrect, run the following command and then use the address that shows up instead:  
`docker inspect m1 | grep "IPAddress"`{{execute}}  
Now you should have a MySQL interface showing. Try to run a MySQL command:  
`show databases;`{{execute}}  
## Fix hashing, DO NOT SKIP THIS STEP
The PHP version we will use and MySQL are experienceing some password hashing compatability issues, unrelated to docker.  
To fix this, for the root user, we need to run the following command in the MySQL interface:  
`ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'guest';`{{execute}}  
## Exit MySQL interface
To exit the MySQL interface, simply use the `exit` command:  
`exit`{{execute}}  
