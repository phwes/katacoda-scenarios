## Docker
Docker containers are a fast and easy way to deploy and test different applications. From a docker image, it only takes a singe command to get an up and running container. While containers are useful for many purposes, they often need to communicate with other hosts or containers. In this tutorial we will set up two containers thay will do just that, communicate with each other.   

## Content
This tutorial will go through:  
  
1. Build and run MySQL from a docker image, using persistent storage for the database.
2. Build and run an apache web server with php from a docker image, using persistent storage for the web pages.
3. Make the containers communicate with each other. 
  
## Disclaimer
This tutorial is just intended for learning and does not apply best practices. For example, the MySQL database will be accessed with the root account, which would be a serious security flaw.
