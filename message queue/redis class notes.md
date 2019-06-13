# Redis introduce

## Why redis

NoSQL, key value

database, cache, middleware

## Redis, memcached and mysql

| product   | database type                   | data storage                             | feature                                                 |
| --------- | ------------------------------- | ---------------------------------------- | ------------------------------------------------------- |
| mysql     | traditional relational database | database, table, field, type             | ACID, master slave copy                                 |
| memcached | in memory cache                 | k/v                                      | high performance, multi-thread                          |
| redis     | in memory + disc                | string, lists, sets, hashes, sorted sets | publish/subscrib, master/slave copy, scale, script[lua] |

# Install Redis

```shell
sudo vi /etc/sysconfig/netword-scripts/ifcfg-ens33
ONBOOT=yes
service network restart
```

环境变量 `echo $PATH`

`$export PATH = $PATH:/sbin`

[Add user sudo](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file-on-ubuntu-and-centos) `sudo usermod -aG wheel username`

更新 `yum upgrade`

`yum install gcc`

ifconfig `yum install net-tools`

wget `yum install wget`

```
cd /usr/local

$ wget http://download.redis.io/releases/redis-5.0.5.tar.gz
$ tar xzf redis-5.0.5.tar.gz
tar -zxvf <file>
$ cd redis-5.0.5
$ make
cd src
make install
./redis-server
```

[关闭服务redis报错 redis (error) ERR Errors trying to SHUTDOWN. Check logs.](https://blog.csdn.net/u013591119/article/details/78149768)

```
cp redis.conf test.conf
sudo vi test.conf
dir /usr/local/redis-5.0.5/
daemonize yes

./redis-server /usr/local/redis-5.0.5/test.conf

./redis-cli -p 6379
```

开机自启

```
cp test.conf /etc/redis/6379.conf
cd utils/
cp redis_init_script /etc/init.d/redisd

vi /etc/init.d/redisd
# chkconfig: 2345 90 10

[root@localhost utils]# service redisd start
/var/run/redis_6379.pid exists, process is already running or crashed

service redisd stop
```

```
delete /var/run/redis.pid file and restart the server again.
```

# Redis data type

设置隔离级别

```sql
set global transaction isolation level repeatable read;
```





