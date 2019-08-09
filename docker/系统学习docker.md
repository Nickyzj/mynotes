##  2-6 在CentOS上安装Docker

### [CentOS Docker 安装](https://www.runoob.com/docker/centos-docker-install.html)

安装完成后 

* `vagrant ssh` 进入虚机
* `vagrant up`创建，启动 
* `vagrant halt` 关机
* `vagrant status`
* `vagrant destroy` 删除

* `docker version`

```shell
sudo yum remove docker docker-common docker-selinux docker-engine
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
sudo yum -y install docker-ce
sudo systemctl start docker
```

* mac `docker-machine version`
* `vagrant destroy` 删除虚机
* `docker-machine create demo` 创建一个安装好 docker 的 linux
* `docker-machine ls` 虚机列表
* `docker-machine ssh demo` 进入虚机
* `docker-machine stop/remove`

#### vagrant fix sudo issue

```shell
sudo groupadd docker
sudo gpasswd -a vagrant docker
sudo service docker restart
```

批量删除 container

```shell
docker rm $(docker container ls -f "status=exited" -q)
```

```
docker container commit # 修改 container 并创建一个新 image
```

```
docker image build # 从 Dockerfile 创建一个 image
```

```
docker exec -it <container id> /bin/bash
```

```
docker exec -it <container id> ip a
```

```
docker container stop <id>
```

```
docker run -d --name=demo <image tag>
docker stop demo
docker start demo
docker ps
docker inspect <container id>
docker logs <container id>
```

安装 Stress

```
docker run -it ubuntu
apt-get update && apt-get install -y stress

```

unknown filesystem type 'vboxsf'

```
vagrant plugin install vagrant-vbguest
vagrant destroy && vagrant up
```

端口

```
sudo docker run --name web -d -p 80:80 nginx
curl 127.0.0.1 
```

docker 开机启动

```
$ sudo systemctl enable docker
To disable this behavior, use disable instead.
$ sudo systemctl disable docker
```

安装 mysql

```
sudo docker run -d -v mysql:/var/lib/mysql --name mysql1 -e MYSQL_ALLOW_EMPTY_PASSWORD=true mysql
sudo docker ps
sudo docker volumn ls
sudo docker volumn rm
```

安装 wordpress

```
docker run -d --name mysql -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=wordpress mysql
docker run -d -e WORDPRESS_DB_HOST=mysql:3306 --link mysql -p 8080:80 wordpress
docker ps

```

docker swarm

```
vagrant ssh swarm-manager
ip a # 获得manger eth1 <ip>
docker swarm init --advertise-addr=<ip>

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-0xy66wp86k9g63obv9gokw1vdiertbbfxbko0b3nsatgfdisfb-3jpbaqb8l9s67jesl39361wqe 10.0.1.52:2377

# worker1
# add worker
docker swarm join --token <token> <ip>:<port>

# manager
docker node ls 
docker service ls
docker service ps demo

# worker
docker ps # 查看活跃容器
docker rm -f <container id> # 强制删除

# manger
docker service rm demo
```

单机部署 wordpress

```
sudo docker run -d -v mysql:/var/lib/mysql --name mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=wordpress mysql
docker ps
docker run -d -e WORDPRESS_DB_HOST=mysql:3306 --link mysql -p 8080:80 wordpress
```





docker swarm 部署 wordpress 

```
# manger
docker network ls
docker network create -d overlay demo
docker service create --name mysql --env MYSQL_ROOT_PASSWORD=root --env MYSQL_DATABASE=wordpress --network demo --mount type=volume,source=mysql-data,destination=/var/lib/mysql mysql
docker service ls
docker service ps mysql

docker service create --name wordpress -p 80:80 --env WORDPRESS_DB_PASSWORD=root --env WORDPRESS_DB_HOST=mysql --network demo wordpress
docker service create --name wordpress -p 80:80 --env WORDPRESS_DB_USER=root --env WORDPRESS_DB_PASSWORD=root --env WORDPRESS_DB_HOST=mysql --network demo wordpress
```

