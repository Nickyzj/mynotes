#Docker 从入门到实践

[https://github.com/Nickyzj/mynotes.git](https://github.com/Nickyzj/mynotes.git)

```
$ docker --version
Docker version 1.12.3, build 6b644ec
$ docker-compose --version
docker-compose version 1.8.1, build 878cff1
$ docker-machine --version
docker-machine version 0.8.2, build e18a919
```
```
docker run -d -p 80:80 --name webserver nginx

这条命令会用 nginx 镜像启动一个容器，命名为 webserver，并且映射了 80 端口，这样我们可以用浏览器去访问这个 nginx 服务器。
```
[http://localhost](http://localhost)

要停止 Nginx 服务器并删除执行下面的命令：
```
$ docker stop webserver
$ docker rm webserver
```
从 Docker Registry 获取镜像的命令是 docker pull。其命令格式为：
```
docker pull [选项] [Docker Registry地址]<仓库名>:<标签>
```
```
$ docker pull ubuntu:14.04
```
```
$ docker run -it --rm ubuntu:14.04 bash

-it：这是两个参数，一个是 -i：交互式操作，一个是 -t 终端。我们这里打算进入 bash 执行一些命令并查看返回结果，因此我们需要交互式终端。

--rm：这个参数是说容器退出后随之将其删除。默认情况下，为了排障需求，退出的容器并不会立即删除，除非手动 docker rm。我们这里只是随便执行个命令，看看结果，不需要排障和保留结果，因此使用 --rm 可以避免浪费空间。

ubuntu:14.04：这是指用 ubuntu:14.04 镜像为基础来启动容器。

bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 bash。
```
要想列出已经下载下来的镜像，可以使用 docker images 命令。
```
$ docker images
```
一般来说，虚悬镜像已经失去了存在的价值，是可以随意删除的，可以用下面的命令删除。

```
$ docker rmi $(docker images -q -f dangling=true)
```

使用 docker exec 命令进入容器，修改其内容。

```
$ docker exec -it webserver bash

root@3729b97e8226:/# echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html

root@3729b97e8226:/# exit

exit

我们以交互式终端方式进入 webserver 容器，并执行了 bash 命令，也就是获得一个可操作的 Shell。

然后，我们用 <h1>Hello, Docker!</h1> 覆盖了 /usr/share/nginx/html/index.html 的内容。
```
```
docker commit \
> --author "Max Zheng" \
> --message "修改了默认网页" \
> webserver \
> nginx:v2
```
```
$docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               v2                  21aa5b826edc        5 seconds ago       109 MB
ubuntu              14.04               2ff3b426bbaa        11 days ago         188 MB
nginx               latest              3448f27c273f        2 weeks ago         109 MB
```
```
$docker history nginx:v2
IMAGE               CREATED              CREATED BY                                      SIZE                COMMENT
21aa5b826edc        About a minute ago   nginx -g daemon off;                            97 B                修改了默认网页
3448f27c273f        2 weeks ago          /bin/sh -c #(nop)  CMD ["nginx" "-g" "daem...   0 B
<missing>           2 weeks ago          /bin/sh -c #(nop)  STOPSIGNAL [SIGQUIT]         0 B
<missing>           2 weeks ago          /bin/sh -c #(nop)  EXPOSE 80/tcp                0 B
<missing>           2 weeks ago          /bin/sh -c ln -sf /dev/stdout /var/log/ngi...   22 B
<missing>           2 weeks ago          /bin/sh -c apt-get update  && apt-get inst...   52.2 MB
<missing>           2 weeks ago          /bin/sh -c #(nop)  ENV NJS_VERSION=1.13.0....   0 B
<missing>           2 weeks ago          /bin/sh -c #(nop)  ENV NGINX_VERSION=1.13....   0 B
<missing>           2 weeks ago          /bin/sh -c #(nop)  MAINTAINER NGINX Docker...   0 B
<missing>           2 weeks ago          /bin/sh -c #(nop)  CMD ["/bin/bash"]            0 B
<missing>           2 weeks ago          /bin/sh -c #(nop) ADD file:a90ec883129f86b...   57.1 MB
```
新的镜像定制好后，我们可以来运行这个镜像。

```
docker run --name web2 -d -p 81:80 nginx:v2
```
