https://coding.imooc.com/class/chapter/305.html#Anchor

https://coding.imooc.com/class/chapter/142.html#Anchor

### 分类

- 负载测试：逐步加压，达到性能阈值，如 cpu 小于80%
- 压力测试：逐步加压，系统某些资源达到饱和，失效
- 并发测试：同一时间，多个虚拟用户同时访问同一模块，同一功能，设置集合点
- 容量测试：数据库层面。获取数据库最佳容量能力。一定的并发用户，不同的基础数据量，观察数据库处理能力，获取数据库各项性能指标
- 可靠性测试：稳定性，高压情况下，系统是否稳定。如 cpu 80%以上，7*24小时运行，是否稳定
- 异常测试：负载均衡，宕机，节点挂掉

### 流程

* 需求分析
  * 明确测试指标
  * 明确测试场景
* 性能指标制定
* 脚本开发
* 场景设置
* 监控部署
* 测试执行
  * 少量用户
* 性能分析
* 性能调优
* 测试报告 

###  性能测试指标

* 事务
* TPS transaction per second
*  并发 （时间范围内，如1秒），没有绝对的并发
  * 多用户系统上进行同一操作
  * 多用户在系统上进行不同操作
  * 同一单位时间内，对系统发起请求用户数

* 吞吐量
  * 一次性能测试网络传输数据量总和
* 点击率

### Linux 监控

top 

vmstat

free

mpstat 查看多核 cpu 每个核心的数据

netstat -ntlp

netstat -i 传输数据大小

iostat 磁盘 cpu

sar

strace

nmon -f -F <filename> -s 1 -c 10 -t

nmon analyzer

crontab

### MySQL

```
(1)QPS(每秒Query量) 
QPS = Questions(or Queries) / seconds 
mysql > show  global  status like 'Question%'; 
 
(2)TPS(每秒事务量) 
TPS = (Com_commit + Com_rollback) / seconds 
mysql > show global status like 'Com_commit'; 
mysql > show global status like 'Com_rollback'; 

线程连接数 'Too many connections...'
show global status like 'Max_used_connections';
show global status like 'Threads%';

最大连接数
show variables like 'max_connections';

Query Cache
查询缓存用于缓存 select 查询结果
下次接收到相同请求，直接返回结果
适用于大量查询，很少改变表内容
修改 my.cnf
query_chach_size, 1024的倍数，32M
query_cache_type=0/1/2
show status like 'Qcache%';
Query_cache_hits
(5)Query Cache命中率 
mysql> show status like 'Qcache%'; 
Query_cache_hits = (Qcahce_hits / (Qcache_hits + Qcache_inserts )) * 100%; 

锁定状态
show global status like '%lock%';
Table_locks_waited/Table_locks_immediate 值越大代表表锁造成阻塞越严重
update操作 where 语句全表搜索是会锁表
innodb_row_lock_waits 行锁，太大可能是间隙锁造成

(8)锁定状态 
mysql> show global  status like '%lock%'; 
Table_locks_waited/Table_locks_immediate=0.3%  如果这个比值比较大的话，说明表锁造成的阻塞比较严重 
Innodb_row_lock_waits innodb行锁，太大可能是间隙锁造成的 
 
(9)复制延时量 
mysql > show slave status 
查看延时时间 
```

### 慢查询

```
/etc/my.cnf
[mysqld]
slow_query_log=1
slow_query_log_file=<path>
long_query_time=1
log_queries_not_using_indexes=1 未使用索引

mysqldumpslow 命令
-s 排序 
    c 访问计数
    l 锁定时间
    r 返回记录
    t 查询时间
    al 平均锁定时间
    ar 平均返回记录数
    at 平均查询时间
-t top N
-g 正则匹配

得到返回记录集最多的10个 sql
mysqldumpslow -s r -t 10 slow.log
访问次数最多的10个 sql
mysqldumpslow -s c -t 10 slow.log
按照时间排序的前10条含左连接的查询语句
mysqldumpslow -s t -t 10 -g "left join" slow.log
```

### explain

```
explain select * from table;
```

### mysql 实时监控

orzdba

lepus 集群监控