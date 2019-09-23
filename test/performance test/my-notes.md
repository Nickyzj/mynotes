centos commands

```
sudo systemctl stop firewalld

netstat -tulnp 看端口

sudo /bin/systemctl start  influxdb.service
sudo /bin/systemctl enable influxdb.service
```



netstat

https://www.thegeekdiary.com/centos-rhel-how-to-find-if-a-network-port-is-open-or-not/



vi /etc/influxdb/influxdb.conf

```
enabled = true
database = "jmeter"
bind-address = ":2003"
protocol = "tcp"
consistency-level = "one"
```

chronograf

[http://centos-server:8888](http://centos-server:8888/)

