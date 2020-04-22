
# Apache web server

## Pull apache image
`docker pull php:7.2-apache`{{execute}}  

## Create persistent storage
`mkdir html`{{execute}}  

## Start and access apache container
Start container...  
`docker run --name a1 -v /root/html:/var/www/html -d -p 8080:80 php:7.2-apache`{{execute}}  
More secure:  
`docker run --name a1 -d -p 127.0.0.1:8080:80 php:7.2-apache`{{execute}}  
Open a tty to the container...  
`docker exec -it a1 /bin/bash`{{execute}}  

## Adapt container environment
`apt update`{{execute}}  
`apt install nano`{{execute}}  
for some reason, this image does not come with the mysqli extension needed for MySQL communication.  
To fix this we run the following commands:  
`docker-php-ext-install mysqli`{{execute}}  
`docker-php-ext-enable mysqli`{{execute}}  
`apachectl restart`{{execute}}  
## Create index page
`nano /var/www/html/index.php`{{execute}}  

#### Easy-access logs
`tail /var/log/apache2/error.log`{{execute}}  
`tail /var/log/apache2/access.log`{{execute}}  
#### Easy-access directories
`cd /var/www/html/`{{execute}}  
`cd /etc/apache2`{{execute}}  
