## Downloading images
Docker is built around so called images...

`docker pull mysql`{{execute}}
`docker pull httpd`{{execute}}

First we will start an MySQL container...
`docker run --name m1 -e MYSQL_ROOT_PASSWORD=guest -d mysql`{{execute}}
