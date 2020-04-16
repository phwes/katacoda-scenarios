
# Apache web server

## Pull apache image
`docker pull httpd`{{execute}}  
Or the one with PHP:  
`docker pull php:7.2-apache`{{execute}}

## Start and access apache container
Start container...  
`docker run --name a1 -d -p 8080:80 httpd`{{execute}}  
More secure:  
`docker run --name a1 -d -p 127.0.0.1:8080:80 httpd`{{execute}}  
Open a tty to the container...  
`docker exec -it a1 /bin/bash`{{execute}}  

## Adapt container environment
`apt update`{{execute}}  
`apt install nano`{{execute}}  
`service apache2 stop`{{execute}}  
`apt install php`{{execute}}  
`service apache2 start`{{execute}}  
`service apache2 status`{{execute}}  
`nano /usr/local/apache2/htdocs/index.html`{{execute}}
`tail /var/log/apache2/error.log`{{execute}}  
`tail /var/log/apache2/access.log`{{execute}}  
`cd /usr/local/apache2/htdocs/`{{execute}}  
