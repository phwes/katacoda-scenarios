
# Apache web server

## Pull apache image
`docker pull php:7.2-apache`{{execute}}

## Start and access apache container
Start container...  
`docker run --name a1 -d -p 8080:80 php:7.2-apache`{{execute}}  
More secure:  
`docker run --name a1 -d -p 127.0.0.1:8080:80 php:7.2-apache`{{execute}}  
Open a tty to the container...  
`docker exec -it a1 /bin/bash`{{execute}}  

## Adapt container environment
`apt update`{{execute}}  
`apt install nano`{{execute}}

## Create index page
`nano /var/www/html/index.php`{{execute}}  

#### Easy-access logs
`tail /var/log/apache2/error.log`{{execute}}  
`tail /var/log/apache2/access.log`{{execute}}  
`cd /usr/local/apache2/htdocs/`{{execute}}  
