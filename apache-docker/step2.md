
# Apache web server

## Pull apache image
`docker pull httpd`{{execute}}

## Start and access apache container
Start container...  
`docker run --name a1 httpd`{{execute}}  
Open a tty to the container...  
`docker exec -it a1 /bin/bash`{{execute}}  
