# Rabbitmq

[windows下 安装 rabbitMQ 及操作常用命令](<https://www.cnblogs.com/ericli-ericli/p/5902270.html>)

```
"C:\Program Files\RabbitMQ Server\rabbitmq_server-3.6.5\sbin\rabbitmq-plugins.bat" enable rabbitmq_management

1、将C:\Users\username\.erlang.cookie 文件复制到 C:\Windows\System32\config\systemprofile 下，替换掉.erlang.cookie。

2、重启rabbitMQ服务

net stop RabbitMQ && net start RabbitMQ

rabbitmqctl.bat list_users

rabbitmqctl.bat add_user username password

rabbitmqctl.bat set_user_tags nicky administrator

rabbitmqctl change_password nicky 123
```

[RabbitMQ console](<http://localhost:15672/>)

