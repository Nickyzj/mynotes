[Exploring Docker](<https://www.youtube.com/watch?v=Kyx2PsuwomE>)

```shell
docker # See all commands
docker version

docker info

# Create first container
# -it run foreground -p public flag
# 80:80 <local>:<container> map port from container to host
# --name <name>
docker container run -it -p 80:80 nginx

docker pull nginx # Pull 
```

[docker hub](<https://hub.docker.com/>)

 ```shell
docker container ls # Show running containers
docker container ls -a # Show all

docker container rm <id> # Remove container
# -f force remove

docker images # Show  images downloaded
docker image rm <id> # Delete image

docker ps # Short way to show running containers

# Create Apache
docker container run -d -p 8081:80 --name myapache httpd

# Create mysql
docker container run -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql

# Stop container
docker container stop mysql

# Bash
docker container exec -it mynginx bash
exit

# Bind folder to container
docker container run -d -p 8080:80 -v $(pwd):/usr/share/nginx/html --name nginx-website nginx

 ```



Dockerfile

```shell
FROM nginx:latest

WORKDIR /usr/share/nginx/html

COPY . . # Everything
```

```shell
docker image build -t <username>/nginx-websit .
docker images # Show the image just built

# Create container use that image 
docker container run -d -p 8082:80 <username>/nginx-websit

# Push image to hub
docker push <username>/nginx-websit

docker login


```

