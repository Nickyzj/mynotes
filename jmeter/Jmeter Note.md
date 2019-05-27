# Jmeter Note

<https://www.blazemeter.com/blog/how-use-jmeter-assertions-three-easy-steps>

bin\jmeter-server` 分布式压测使用的启动文件

`jmeter.properties` 配置文件

## Thread Group

* Number of Threads
* Ramp-up Period
* Loop Count <forever>

## HTTP Sampler

### Add > Sampler > Http Request

* protocol
* IP, port
* Method
* Path
* Redirects
* Use keepalive
* use multipart/form-data for POST
* browser-compatible headers



## Result Tree

* load time
* latency
* size
* response code

### Request

#### post

paramters



### Response

### Aggregate Report



## Assertion

### Response assertion

* **Text response -** This is for the response that can be displayed in a browser
* **Document (text) -** This is for anything supported by [Apache Tika](http://tika.apache.org/1.2/formats.html) (it assumes the presence of apache-tika.jar in /lib folder of a JMeter installation). This can include PDF, Office, audio, and video formats. Be careful, because this can be memory-intensive for high loads.
* **URL Sampled -** This assertion is used against a requested URL to ensure it matches expectations. For example, you may want to check that the redirect URL doesn’t contain an error somewhere in the path.
* **Response Code -** This checks to ensure the response code is expected. For 4xx and 5xx response codes, make sure you have checked the “Ignore Status” box (see below for a full explanation).
* **Response Message -** This verifies that the response message appears as  expected.
* **Response Headers -** This is used against Response Headers to see if a specific HTTP header is present or absent.
* **Ignore Status -** JMeter out-of-the-box considers all 4xx and 5xx responses as failures. If your test case is negative and, for example, a 404 error is expected, you’ll check this box to suppress JMeter’s built-in status code check and substitute it with your own status code assertion.

## User define Paramter

`Add > config element > user defined paramter`

`${name}`

## CSV data set config

| user1 | password1 |
| ----- | --------- |
| user2 | password2 |
| user3 | password3 |

* filename
* varaible names
* delimeter
* sharing mode

## Mysql

mysql-connector-java-5.1.30.jar

`add > sampler > jdbc request`

`add > config element > jdbc connection configuration`

`jdbc:mysql://127.0.0.1:3306/blog`

`jdbc driver class: com.mysql.jdbc.Driver`

`test plan > add directory or jar to classpath`

`jdbc request 中 variable name of pool declared in jdbc connection configuration 必须和 jdbc connection configuration 中的名称相同`

query type

* prepared statement

## 分布式压测

master (controller) / server (generator)

master will send script to server

执行的时候，server上只要把 jmeter-server 打开，不要启动jmeter

结束后，server 会把数据回传 master, master 输出报告

`bin/jmeter.properties`

`remote_hosts=<ip>:<port>, <ip>:<port>`

`server_port=8899`

`scp -r <source file> <user>@<ip>/<path to dest>`

`./jmeter-server` or

`nohup ./jmeter-server &`

`ps -ef | grep jemter-server`

`ps  aux | grep jemter-server`



## Non GUI

```
cd jmeter
wget <url>
tar -zxvf <file>
```

## Best practice

1. 使用非GUI

   `jmeter -n -t test.jmx -l result.jtl`

2. 少使用listener。如果使用 -l 它们可被删除或禁用
3. 测试期间不要使用tree view 或 查看结果 监听器，只用来调试脚本
4. 少使用断言
5. 测试大量数据，以csv read方式读取
6. 多节点

## Test report dashboard

`jmeter -n -t <path/file.jmx> -l <path/result.jtl> -e -o <result path>`



## 总结

1. 缓存命中率
2. 缓存容量
3. 缓存淘汰算法LRU
4. 内网压测，排除带宽
5. JVM垃圾回收GC策略调整
6. 数据库连接池 mysql server 3000 - 4000
7. 数据库索引设计，字段是否合理
8. 缓存或数据库慢查询分析
9. 数据库设计，分库分表，水平分，垂直分
10. 数据库读写分离
11. response time 响应时间
12. cpu 占用率
13. 内存使用率
14. 接口http成功率
15. 配置元件 》前置处理器 》定时器 》采样器 》后置处理器 》断言 》监听器