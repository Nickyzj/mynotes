https://www.howtoing.com/how-to-install-and-configure-zabbix-to-securely-monitor-remote-servers-on-ubuntu-18-04



### How to install Zabbix Agent 4.2 ? Ubuntu, RHEL, CentOS

https://zabbixonly.com/how-to-install-zabbix-agent-4-2-ubuntu-rhel-centos/



### grafana

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



### CentOS7查看和关闭防火墙

https://blog.csdn.net/ytangdigl/article/details/79796961



http://10.0.0.25/zabbix/zabbix.php?action=dashboard.view

http://192.168.1.10/zabbix/zabbix.php?action=dashboard.view

Admin/zabbix





/usr/local/var/lib/grafana/plugins/



/Users/jizheng/Documents/tools/grafana



### mac agent

```

# config
/usr/local/etc/zabbix/zabbix_agentd.conf

# start
/usr/local/sbin/zabbix_agentd
```

http://blog.oper-init.eu/2016/07/05/install-zabbix-agent-on-mac-osx/



### centos

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



### mysql

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



### centos mysql

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



steps for centos intall zabbix

https://www.zabbix.com/documentation/4.0/zh/manual/installation/install_from_packages/rhel_centos

https://tecadmin.net/install-zabbix-agent-on-centos-rhel/



[https://www.centos.bz/2018/04/zabbix-%E7%9B%91%E6%8E%A7-nginx-status-%E6%80%A7%E8%83%BD-2/](https://www.centos.bz/2018/04/zabbix-监控-nginx-status-性能-2/)

http://ubuntu-server/basic_status



```

systemctl start httpd

http://centos-server/zabbix/

/etc/zabbix/scripts/nginx.sh

sudo vi /etc/nginx/nginx.conf

sudo systemctl restart zabbix-agent

sudo nginx -s reload
```



### tomcat install

https://www.vultr.com/docs/how-to-install-apache-tomcat-8-on-centos-7

```
yum install -y zabbix-java-gateway

vim /etc/zabbix/zabbix_java_gateway.conf

systemctl start zabbix-java-gateway.service

vim /etc/zabbix/zabbix_server.conf

vi /opt/tomcat/bin/setenv.sh

netstat -anlp | grep 9000
```

https://www.cnblogs.com/ssgeek/p/9299273.html

https://geekflare.com/enable-jmx-tomcat-to-monitor-administer/

```
CATALINA_OPTS="-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9000 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false -Djava.rmi.server.hostname=192.168.15.74"

CATALINA_OPTS="-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9000 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false -Djava.rmi.server.hostname=10.0.0.20"
```

```
java -jar cmdline-jmxclient-0.10.3.jar - centos-server2:9000 java.lang:type=Memory NonHeapMemoryUsage
```

https://my.oschina.net/u/2338224/blog/1793153



```
JMeterPluginsCMD.sh --generate-png perfmon_result_cpu.png --input-jtl perfmon_result_cpu.jtl --plugin-type PerfMon --width 800 --height 600
JMeterPluginsCMD.sh --generate-png perfmon_result_memory.png --input-jtl perfmon_result_memory.jtl --plugin-type PerfMon --width 800 --height 600
JMeterPluginsCMD.sh --generate-png perfmon_result_network.png --input-jtl perfmon_result_network.jtl --plugin-type PerfMon --width 800 --height 600
```

### jmeter perfmon agent

```
/home/root/ServerAgent
./startAgent.sh
```

jmeter guide

https://octoperf.com/blog/2017/10/19/how-to-analyze-jmeter-results/



### 启动 zabbix server

```
systemctl start httpd
systemctl start zabbix-server
systemctl start zabbix-agent
systemctl start zabbix-java-gateway
ntpdate us.pool.ntp.org

```

zabbix-java-gateway

https://jaminzhang.github.io/monitoring/Zabbix-config-JMX/

```
vi /etc/zabbix/zabbix_java_gateway.conf
```

### run jmeter test

```
jmeter -n -t tomcat.jmx -l test_result/hpbook_tomcat_10user_1 -e -o test_result/hpbook_tomcat_10user_report_1

jmeter -n -t tomcat.jmx -l test_result/hpbook_tomcat_60user_1 -e -o test_result/hpbook_tomcat_60user_report_1 -Jtest_name=hpbook_tomcat_60user -Jusers=60 -Jramp_up=120
```

https://www.cnblogs.com/dreamanddead/p/why-should-you-set-hostname-in-jmeter-distribute-test.html

system.properties最后一行添加，

```
java.rmi.server.hostname=192.168.1.4
```

jmeter 坑

https://testerhome.com/topics/10950