
# Apache web server

## Pull apache image
`docker pull httpd`{{execute}}

## Start and access apache container
Start container...  
`docker run --name a1 -d -p 8080:80 httpd`{{execute}}  
More secure:  
`docker run --name a1 -d -p 127.0.0.1:8080:80 httpd`{{execute}}  
Open a tty to the container...  
`docker exec -it a1 /bin/bash`{{execute}}  
