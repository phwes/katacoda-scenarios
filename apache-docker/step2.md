
# Apache web server
You rarely use just a database without any other service accessing it. For this tutorial Apache web server will be the one to access and use the MySQL database. Apache has its own docker image `httpd`, but it comes without php support. Therefore we will use the php image version `php:7.2-apache` instead. This image comes with both apache and php. Sadly the image seems to miss the impartant module `mysqli`, but we will fix that in one of the steps below. 

## Pull apache image
`docker pull php:7.2-apache`{{execute}}  

## Start and access apache container
Start container...  
`docker run --name a1 -v /root/html:/var/www/html -d -p 8080:80 php:7.2-apache`{{execute}}  
With link:  
`docker run --name a1 --link m1:mysql-server -v /root/html:/var/www/html -d -p 8080:80 php:7.2-apache`{{execute}}  
Just like when we started the MySQL container, we want to use additional parameters when starting the apache container. 
`docker run --name a1 --link m1:mysql-server -mount /root/html:/var/www/html -d -p 8080:80 php:7.2-apache`{{execute}}  
As you probably noticed, we received an error while running the previous command. That is because we used `--mount` insted of `-v`. While docker volumes will create the directory for you, bind mounts will give you an error if the directory exists. While the two parameters come from different backgrounds, this is the key difference in docker at the moment.  
So create the directory  
`mkdir html`{{execute}}  
and run the command again  
`docker run --name a1 --link m1:mysql-server -mount /root/html:/var/www/html -d -p 8080:80 php:7.2-apache`{{execute}}  

## Open a shell to the container
Sometimes you would like to enter the environment with a shell. To do this we run bash from within the container with the `docker exec` command. But without parameters this shell would be daemonized like the container, so to make it interactive for us we add the `-it` paramter:    
`docker exec -it a1 /bin/bash`{{execute}}  

## Adapt container environment
`apt update`{{execute}}  
`apt install nano`{{execute}}  

### Install mysqli 
For php to establish a connection to the MySQL database, it needs the mysqli extension. But foror some reason, this image does not come with the extension and therefor we have to download it with the `docker-php-ext` commands supplied to us by the php image:  
`docker-php-ext-install mysqli`{{execute}}  
`docker-php-ext-enable mysqli`{{execute}}  
`apachectl restart`{{execute}}  
## Create index page
I have supplied you with a couple of test php-pages that can be used for the apache server.  
Let us begin by moving the php testpage to our bind point:  
`mv test.txt html/index.php`{{execute}}  
Click the + sign in the toolbar of the terminal and `select port to view on Host1`. Then enter the port on our host machine that is connected to the apache container (8080). You should now see a php information page. 
