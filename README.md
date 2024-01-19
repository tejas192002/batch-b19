Docker
Docker Installation on Ubuntu
ref: https://docs.docker.com/engine/install/ubuntu/

# Docker Commands
## ######### WORK WITH CONTAINERS #############

docker run <docker-image>   # Run docker container

docker run -d <docker-image>    # run docker container in dettached way

docker ps   # to list running containers

docker ps -a    # to list all containers

docker inspect <container_id>   # get detailed info about container

docker run -d -p <host-port>:<container-port> <docker-image>    # map host machine port 
to container port to expose application on host machine

docker run -it <docker-image> bash  # to access new container terminal 

docker exec -it <container-id> bash     # to access running container terminal

docker exec -it <container-id> <command>    # to execute command inside the container

docker cp <source> <destination>    # to copy file from host machine to container OR conrainer to host machine OR container to container

docker run -d --name <container-name> <docker-image>    # to run container with name

docker run -d -P nginx  # to map container port on random host machine port range from 32768.

docker create <docker-image>    # to create the container

docker start <container-id>     # to start the container

docker stop <container-id>      # to stop the container

docker rm <container-id>    # to remove the stoped container

docker rm -f <container-id>    # to remove the container forcefully

docker logs <container-id>  # check docker logs

docker container stats      # to see container resources utlization

docker rm -f `docker ps -aq`   # to remove all containers

## ########### WORKING WITH CONTAINER IMAGES ###########

docker images   # to list docker images

docker image list   # to list docker images

docker pull <IMAGE-NAME>    # to pull docker image

docker rmi <image-name>     # to remove docker unused image. use -f for forcefully.

docker image rm <image-name>    # to remove docker unused image. use -f for forcefully.

docker commit <container-id>    # to save changes from container to new image

docker tag <image-id> <new-image-name>  # to rename the image

docker login    # to authenticate in docker hub

docker push <repo-name>     # push image in registry

docker save -o <file-name>.<tar/zip> <image-id>     # archive image

docker load -i <file-name>              # extract image from archive

## Docker Network Drivers
ref: https://docs.docker.com/network/drivers/

docker network list     # to list the network

docker network create --drive=<driver> --subnet=<subnet-cidr> <network-name>    # to create docker network

docker run --network=<network-name> <image-name>    # to run container in specific network

docker network rm <network-name>    # to remove the network

## Docker Volume

docker volume list      # to list volumes

docker volume create <vol-name>     # to create volume

docker run -v <vol-name>:<mount-path> <image>   # to run container with volume

## Deploy three tier Application using Docker

step1: Deploy DB container
docker volume create studentapp-vol
docker run -d -v studentapp-vol:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=redhat mysql
docker exec -it mysql bash [mysql create database studentapp;] [create_schema]

step2: Deploy backend container
configure context.xml
update dockerfile
build backend image
docker run -d -p 8080:8080 backend:latetest

step3: Deploy frontend container
configure index.html (update backend url)
build frontend image
docker run -d -p 80:80 frontend:latest
 
test file 1