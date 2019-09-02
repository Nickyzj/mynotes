https://www.howtoing.com/how-to-install-and-configure-zabbix-to-securely-monitor-remote-servers-on-ubuntu-18-04



How to install Zabbix Agent 4.2 ? Ubuntu, RHEL, CentOS

https://zabbixonly.com/how-to-install-zabbix-agent-4-2-ubuntu-rhel-centos/



grafana

```
/Users/jizheng/Documents/tools
```

```
grafana-server --config=/usr/local/etc/grafana/grafana.ini --homepath /usr/local/share/grafana cfg:default.paths.logs=/usr/local/var/log/grafana cfg:default.paths.data=/usr/local/var/lib/grafana cfg:default.paths.plugins=/usr/local/var/lib/grafana/plugins
```

```shell
./grafana-server cfg:default.paths.plugins=/usr/local/var/lib/grafana/plugins
```

http://localhost:3000/?orgId=1

admin/admin



CentOS7查看和关闭防火墙

https://blog.csdn.net/ytangdigl/article/details/79796961



http://10.0.0.25/zabbix/zabbix.php?action=dashboard.view

http://192.168.1.10/zabbix/zabbix.php?action=dashboard.view

Admin/zabbix





/usr/local/var/lib/grafana/plugins/



/Users/jizheng/Documents/tools/grafana



mac agent

```

# config
/usr/local/etc/zabbix/zabbix_agentd.conf

# start
/usr/local/sbin/zabbix_agentd
```

http://blog.oper-init.eu/2016/07/05/install-zabbix-agent-on-mac-osx/



centos

```
/etc/zabbix/zabbix_agentd.conf
# start up
service zabbix-agent start
```

ubuntu

```
sudo systemctl start zabbix-agent

日志
/var/log/zabbix
```



mysql

```
grant usage on *.* to zabbix@127.0.0.1 identified by '123456';
flush privileges;

/etc/zabbix/下创建一个包含MySQL用户名和密码的配置文件“.my.cnf”
[client]
user=zabbix
host=127.0.0.1
password=123456

HOME=/usr/local/etc/zabbix mysqladmin ping | grep -c alive

[client]
user=nicky
host=127.0.0.1
password=123123

HOME=/etc/zabbix mysqladmin ping | grep -c alive
```

```
UserParameter=mysql.status[*],/usr/local/etc/zabbix/zabbix_agentd.conf.d/check_mysql $1
UserParameter=mysql.ping,HOME=/usr/bin/mysqladmin ping 2>/dev/null | grep -c alive
UserParameter=mysql.version,/usr/bin/mysql -V
```



centos mysql

```
yum install -y mariadb-server
systemctl start mariadb.service

#重启mariadb
systemctl restart mariadb.service

#重启zabbix agent
systemctl restart zabbix-agent.service

zabbix配置数据库连接时出现：Error connecting to database: Can’t connect to local MySQL server through socket ‘/var/lib/mysql/mysql.sock’ (13)
关闭当前的selinux:
setenforce 0
查看selinux状态
getenforce
注意错误代码(13)表示你的系统selinux没有关
sed -i '/SELINUX/s/enforcing/disabled/' /etc/selinux/config
```

```
my.cnf (my.ini on windows)

#Replace xxx with your IP Address 
bind-address        = xxx.xxx.xxx.xxx
then

CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypass';
CREATE USER 'myuser'@'%' IDENTIFIED BY 'mypass';
Then

GRANT ALL ON *.* TO 'myuser'@'localhost';
GRANT ALL ON *.* TO 'myuser'@'%';
flush privileges;
```

