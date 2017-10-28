# dockerWordPress
1.	Install Docker compose from https://docs.docker.com/compose/install/#prerequisites
for linux
sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

REM: Check the compatibility matrix after writing the docker compose file.
To remove docker-compose : sudo rm /usr/local/bin/docker-compose
 
2.	If docker is required to upgrade, then follow here
https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/
sudo apt-get remove docker docker-engine docker.io
sudo apt-get update
sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual

Install Docker-CE
Setup repo
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce
sudo docker run hello-world
 
3.	Start docker image for wordpress site.
https://docs.docker.com/compose/wordpress/
cat > docker-compose.yml
 
version: '3'
services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress
wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
volumes:
    db_data:


docker-compose up -d

Now access the url.

