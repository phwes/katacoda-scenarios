
# Apache web server
You rarely use a database without any other service accessing it. For this tutorial Apache web server will be the one to access and use the MySQL database. Apache has its own docker image `httpd`, but it comes without php support. Therefore we will use the php image version `php:7.2-apache` instead. This image comes with both apache and php. Sadly the image seems to miss the important module `mysqli`, but we will fix that in one of the steps below. 

## Pull apache image
`docker pull php:7.2-apache`{{execute}}  

## Start and access apache container
Just like when we started the MySQL container, we want to use additional parameters when starting the apache container. In addition to parameters we used for the MySQL container, we will use:  
* `--link`, the link parameter creates a link between docker containers. While our apache container certainly would be able to communicate with our MySQL container without a link, the IP address might change. So instead we use a link that adds and maintains a reference to our MySQL container in the /etc/hosts file.   
* *`-p`*, this parameter maps a host port to a container port. By using this parameter you can host multiple applications that, from the perspective of the container, listen at the same port. But outside of the container, the application is accessed on whatever port the host machine has been assigned to forward from. We will let the port 8080 on the host machine map to the 80 port on the apache container.  

Let us start the container:  
`docker run --name a1 --link m1:mysql-server -v /root/html:/var/www/html -d -p 8080:80 php:7.2-apache`{{execute}}  

## Open a shell to the container
Sometimes you would like to enter the environment with a shell. To do this, we will run the bash command from within the container, with the `docker exec` command. But without parameters this shell would be daemonized like the container, so to make it interactive for us we add the `-it` paramter:  
`docker exec -it a1 /bin/bash`{{execute}}  

### Install mysqli 
For php to establish a connection to the MySQL database, it needs the mysqli extension. But for some reason, this image does not come with the extension and therefore we have to download it with the `docker-php-ext` commands supplied to us by the php image:  
`docker-php-ext-install mysqli`{{execute}}  
  
`docker-php-ext-enable mysqli`{{execute}}  
  
`apachectl restart`{{execute}}  
You will get a message about the server's domain name, but you can ignore it.
## Create index page
I have supplied you with a couple of test php-pages that can be used for the apache server.  
Let us begin by moving the php testpage to our volume, so the container can access it:  
`mv test.txt html/index.php`{{execute}}  
Click the + at the top of the terminal and `select port to view on Host1`. Then enter the port on our host machine that is connected to the apache container (8080). You should now see a php information page. 
