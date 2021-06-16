# Docker-Compose-WordPress
Docker-compose file for creating WordPress website with SSL


# Description

Here I have created a sample docker-compose file for creating a WordPress website with SSL certificate. This docker-compose file will create 3 docker containers,
1. Database - MySQL container with wordpress database
2. WordPress - Wordpresss + php-fpm container
3. Nginx - Nginx Container

Here custom configuration file is added for Nginx to use the WordPress container for the php-fpm requests and for adding SSL certificate. All the connections between the containers are internal using a custom docker network and the databases and WordPress files are stored using docker volumes. The docker network and docker volumes will be also created by the docker-compose file. Here I have used a self-signed SSL certificate only. You can add your SSL certificate by editing the 'ssl.crt' and 'ssl.key' files. 

## How to use

```
1. Install docker-compose
# curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# chmod +x /usr/local/bin/docker-compose

2. Clone this Repo to your server
# git clone https://github.com/MarkAntonyGit/Docker-Compose-WordPress.git
# cd Docker-Compose-WordPress

3. Add your SSL certificate and Private Key to the ‘ssl.crt’ and ‘ssl.key’ files.

4. Run following command to start the Containers
# docker-compose up -d
```

This is it! Your new Docker WordPress website is now ready to install. 

## Code Breakdown

A docker-compose file mailny have 4 sections,


1.Version
----------
Here we enter the docker version,
```
Eg: version: "3"
```

2.Services
----------

Here we enter the parameters needed for required containers, In this docker-compose file I have added 3 docker containers like below,

```
Eg: 

services:
  database:                 >>>>>> MySQL Container Section
    image: mysql:5.6                  
    container_name: database             
    restart: always 
      .....
  wordpress:               >>>>>>> WordPress Container Section
    image: wordpress:php7.4-fpm-alpine
    container_name: wordpress
    depends_on:
      - database
      .....
  nginx:                   >>>>>>>> Nginx Container Section
    image: nginx:alpine
    container_name: nginx
    depends_on:
      - wordpress
    restart: always
      ....
```   
3.Volumes
---------

Here we add the volumes needs to be created for the containers. For this I have used 2 volumes, one for MySQL databases and One for WordPress Document root.

```
volumes:
  wordpress-vol:
  mysql-vol:
```

4.Networks
----------

Here we add the Docker network needed for the containers
```
networks:
  wpnet:
```
#### Sample Screenshots

-- Docker Containers 

![](https://raw.githubusercontent.com/MarkAntonyGit/MarkAntonyGit/main/Uploads/Docker/3.JPG)

-- Sample Website

![](https://raw.githubusercontent.com/MarkAntonyGit/MarkAntonyGit/main/Uploads/Docker/2.JPG)

-- Sample Self Signed SSL

![](https://raw.githubusercontent.com/MarkAntonyGit/MarkAntonyGit/main/Uploads/Docker/1.JPG)

### Connect with me

--------<img src="https://img.shields.io/badge/-Mark%20Antony-brightgreen"/> ----------------------------------------------------------------------------------------------------------------------------------- <a href="https://www.linkedin.com/in/profile-markantony/"><img src="https://img.shields.io/badge/-Linkedin%20Profile-blue"/></a> ------------------------------------------------------------------------------------------------------------------------------------ <a href="mailto:markantony.alenchery@gmail.com"><img src="https://img.shields.io/badge/-markantony.alenchery@gmail.com-D14836?style=flat&logo=Gmail&logoColor=white"/></a>-------------------------------------------------------
