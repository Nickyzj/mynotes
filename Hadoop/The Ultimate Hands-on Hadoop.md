# [The Ultimate Hands-on Hadoop](https://learning.oreilly.com/videos/the-ultimate-hands-on/9781788478489)

safarinicky01

[Extract Transform Load](https://www.youtube.com/watch?v=K_FCHYWGGug)

* data connectivity
* performance
* transformation flexibility
* data quality
* flexible data acquisition options
* committed vendor to ETL

[What is Hadoop?: SQL Comparison](https://www.youtube.com/watch?v=MfF750YVDxM)

* **Schema On Read** instead of **Schema On Write**

[Learn MapReduce with Playing Cards](https://www.youtube.com/watch?v=bcjSe0xCHbE)

HDFS

* breaks large files into smaller chunks(blocks)
* various nodes can operate on different chunks of the same file at the same time
* when finished, all the data is combined based on the key
* far more efficient than one node operating on a single file
* scales linearly

[What is OLAP?](https://www.youtube.com/watch?v=2ryG3Jy6eIY)

## Ch1: learn all the buzzwords. and install hadoop

[Hadoop Ecosystem Explained in 20 min](https://www.youtube.com/watch?v=DCaiZq3aBSc)

- the hadoop ecosystem
  * run on an entire cluster of PCs
  * distributed storage (redundant), automatically recover
  * distributed processing (aggregate data in a parallel manner)
  * commodity hardware

* Hadoop history

  Google File System

* why hadooop?
  * data is too big TB per day
  * vertical scaling doesn't cut it
    * disk seek times
    * hardware failures
    * processing times
  * horizontal scaling is linear
  * parallel processing

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-23%20at%2010.28.18%20PM.png?raw=true)

Hadoop Distributed File System

**YARN**: data storage, data processing

* what gets to run tasks when
* what nodes are available for extra work, which nodes are not
* which ones are available

**MapReduce**

* programming model, process your data across an entire cluster
* mappers, and reducers
* mappers: transform data in parallel across your cluster
* reducers: aggregate data together

**Pig**, SQL style syntax (no python or java)

**Hive**: looks like a sql database. take sql queries

**Apache Ambari**: visualize what's running on cluster, system resources, execute hive queries, import databases into hive, execute pig queries

**MESOS**: alternative to YARN

**Spark**: run queries on data, machine learning, handle streaming data in real time. Python or Java or Scala

**TEZ**: 

**HBase**: nosql database. Fast. Can be hitting from website

**Apache STORM**: process streaming data

**OOZIE**: scheduling jobs

**Zookeeper**: coordinating everything on cluster

**SCOOP**: a connector, Hadoop database to relational database (ODBC, JDBC)

**Flume**: transform web logs to cluster

**Kafka**: collect data from cluster of PCs or web servers and broadcase into hadoop



https://learning.oreilly.com/videos/the-ultimate-hands-on/9781788478489/9781788478489-video1_1

https://www.cloudera.com/downloads/hortonworks-sandbox/hdp.html

https://grouplens.org/datasets/movielens/ 

## Ch2: using Hadoop's Core: HDFS and MapReduce

### HDFS: What it is, and how it works

* handles big files
* by breaking them into blocks (128MB)
  * distributed processing
* stored across several commodity computers 

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%209.09.38%20AM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%209.11.18%20AM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%209.12.49%20AM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%209.16.39%20AM.png?raw=true)

* namenode resilience
  * back up metadata
    * namenode writes to local disk and NFS
  * secondary namenode
    * maintains merged copy of edit log you can restore from
  * HDFS federation
    * each namenode manages a specific namespace volume
  * HDFS high availability 
    * hot standby namenode using shared edit log
    * zookeeper tracks active namenode
    * uses extreme measures to ensure only one namenode is used at a time

* Using HDFS
  * UI (Ambari)
  * Command LIne Interface
  * HTTP / HDFS Proxies
  * Java interface
  * NFS Gateway

### install dataset into HDFS using command line

```shell
hadoop fs -ls
hadoop fs -mkdir <dir name>
hadoop fs -copyFromLocal <local file> <hdfs file path>
hadoop fs -ls <hdfs file path>
hadoop fs -rmdir <dir name>
hadoop fs # List all command
```

### MapReduce: What it is, and how it works

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%205.48.43%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%205.50.42%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%205.51.55%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%205.52.37%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%205.53.35%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.09.14%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.11.36%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.13.02%20PM.png?raw=true)

### How MapReduce distributes processing

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.14.55%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.18.46%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.22.35%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.23.59%20PM.png?raw=true)

### MapReduce example: Break down movie ratings by rating score

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.28.36%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.31.08%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.34.04%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.35.29%20PM.png?raw=true)

### [Activity] Installing Python, MRJob, and nano

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.38.57%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-24%20at%206.45.57%20PM.png?raw=true)

### [Exercise] Rank Movies by their popularity

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2010.20.03%20AM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2010.22.14%20AM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2010.24.39%20AM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2010.25.37%20AM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2010.28.02%20AM.png?raw=true)

### [Activity] Check your results

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2010.35.24%20AM.png?raw=true)

**shuffle and sort stage in mapper. will sort by key automatically.**

## Ch3: Programming Hadoop with Pig

```shell
su root
ambari-admin-password-reset
```

### Introducing Pig

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2012.38.26%20PM.png?raw=true)

MapReduce: mapper, reducer - mapper, reducer… linear way

TEZ: much faster

### Running Pig

* Grunt
* Script
* Ambari / Hue

### An example

* find the oldest 5-start movies

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2012.44.23%20PM.png?raw=true)

name it (schema) when load

4 elements tuple.

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2012.47.20%20PM.png?raw=true)

dump metadata # Output

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2012.53.00%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2012.55.30%20PM.png?raw=true)

- create bag in pig
- contains tuples of all individuals of rows
- associated with given movie id
- similiar to a reducer

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%2012.57.22%20PM.png?raw=true)

* generate -> generate new rows
* AVG go through everything in bag

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%201.03.53%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%201.05.02%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%201.06.54%20PM.png?raw=true)

 ![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%201.09.00%20PM.png?raw=true)

### more Pig Latin

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%201.41.19%20PM.png?raw=true)

* load -> reading, store -> writing

### Diagnostics

* DESCRIBE
* EXPLAIN
* ILLUSTRATE

### UDF'S

* REGISTER
* DEFINE
* IMPORT

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%205.27.19%20PM.png?raw=true)

### [Exercise] Find the most-rated one-star movie

Defining the problem

* find all movies with an average rating less than 2.0
* sort them by the total number of ratings

Hint

* new thing COUNT(). count up the number of items in a bag. Just like AVG

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%205.37.10%20PM.png?raw=true)

## Ch4: Spark

"A fast and general engine for large-scale data processing"

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.05.18%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.06.34%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.07.33%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.08.17%20PM.png?raw=true)

resilient 弹性

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.09.02%20PM.png?raw=true)

* Spark Streaming: input data in real time
* MLLib: machine learning
* GraphX: 

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.13.35%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.15.08%20PM.png?raw=true)

### The Resilient Distributed Datasets(RDD)

* Resilient
* Distributed
* Dataset

### The sparkContext

* created by your driver program
* is responsible for making RDD's resilient and distributed
* creates RDD's
* the spark shell creates a "sc" object for you

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.18.06%20PM.png?raw=true)

### Transforming RDD's

* map
* flatmap
* filter
* distinct
* sample
* union, intersection, subtract, cartesian

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.24.25%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.26.39%20PM.png?raw=true)

### RDD actions

* collect
* count
* countByValue
* take
* top
* reduce
* ...

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%206.29.19%20PM.png?raw=true)

### [Activity] Find the movie with the lowest average rating - with RDD's

### Datasets and Spark 2.0

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%209.27.33%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%209.30.06%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%209.31.39%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%209.33.16%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%209.34.11%20PM.png?raw=truehttps://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%209.34.38%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-25%20at%209.34.38%20PM.png?raw=true)

## CH5: Relational Data stores with Hadoop

### HIVE

- Distributing SQL queries with Hadoop
- Translates SQL queries to MapReduce or Tez jobs on your cluster
- HiveQL
- Easy OLAP queries
- Highly extensible
  - User defined functions
  - Thrift server
  - JDBC/ODBC driver

Why not Hive?

* High latency - not appropriate for OLTP
* Stores data de-normalized
* SQL is limited in what it can do
  * Pig, Spack allows more complex stuff
* No transactions
* No record-level updates, inserts, deletes

HiveQL

* MySQL with some extensions
* views
* allows to specify how structured data is stored and partitioned

### [Activity] Use Hive to find the most popular movie

* Ambari -> Hive view -> upload data file

```sql
CREATE VIEW topMovieIDs IF NOT EXISTS AS
SELECT moveID, count(movieID) as ratingCount
FROM ratings
GROUP BY movieID
ORDER BY ratingCount DESC;

SELECT n.title, ratingCount
FROM topMoviesIDs t JOIN names n ON t.movieID = n.movieID;

DROP VIEW topMovieIDs;
```

### How Hive Works

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.28.00%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.32.10%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.41.18%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.43.18%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.46.00%20PM.png?raw=true)

```sql
CREATE VIEW IF NOT EXISTS avgRatings AS
SELECT moveID, AVG(rating) as avgRating, COUNT(movieID) as ratingCount
FROM ratings
FROUP BY movieID
ORDER BY avgRating DESC;

SELECT n.title, avgRating
FROM avgRating t JOIN name n ON t.movieID = n.movieID
WHERE ratingCount > 10;
```

### Integrating MySQL with Hadoop

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.51.21%20PM.png?raw=true)

#### sqoop

* sqoop can candle big data

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.52.44%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.53.52%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.55.52%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.56.30%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.57.14%20PM.png?raw=true)

* -m 1 means one mapper

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%201.59.13%20PM.png?raw=true)

```sql
mysql -u root -p hadoop
create database movielens;
show databases;
exit

wget http://media.sundog-soft.com/hadoop/movielens.sql

mysql -u root -p hadoop
SET NAMES 'utf8';
SET CHARACTER SET utf8;

use movelens;
source movielens.sql;
show tables;

select * from movies limit 10;

describe ratings;

select movies.title, count(ratings.movie_id) as ratingCount
from movies
inner join ratings
on movies.id = ratings.movie_id
group by movies.title
order by ratingCount;
```

### [Activity] Use Sqoop to import data from MySQL to HFDS/Hive

```sql
mysql -u root -p hadoop
grant all privileges on movielens.* to ''@'localhost';
```

```shell
sqoop import --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --table movies -m 1
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%202.13.05%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%202.13.29%20PM.png?raw=true)

```shell
sqoop import --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --table movies -m 1 --hive-import
```

### [Activity] Use Sqoop to export data from Hadoop to MySQL

```sql
mysql -u root -p hadoop
use movielens;
create table exported_movies (id integer, title varchar(255), releaseDate DATE);
exit;

sqoop export --connect jdbc:mysql://localhost/movielens -m 1 --dirver com.mysql.jdbc.Driver --table exported_movies --export-dir /apps/hive/warehouse/movies --input-fields-terminated-by '\0001'

mysql -u root -p hadoop
use movielens;
select * from exported_movies limit 10;
```

## CH6: non-relational data stores

### HBase

* Built on HDFS

* Create, Read, Update, Delete. 
* No query language

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.06.07%20PM.png?raw=true)

* region server. Ranges of keys. partitioning.
* app talks to region server.

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.10.23%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.12.59%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.17.07%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.40.41%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.42.35%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.45.04%20PM.png?raw=true)

```shell
maria_dev
su root
/usr/hdp/current/hbase-master/bin/hbase-daemon.sh start rest -p 8888 --infoport 8001
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.49.40%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.54.56%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.55.50%20PM.png?raw=true)

```shell
/usr/hdp/current/hbase-master/bin/hbase-daemon.sh stop rest
```

### [Activity] Use HBase with Pig to import data at scale

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%203.57.52%20PM.png?raw=true)

```shell
root
hbase shell
list
create 'users', 'userinfo'
list
exit

wget http://media.sundog-soft.com/hadoop/hbase.pig

```

```shell
users = LOAD '/user/maria_dev/ml-100k/u.user' 
USING PigStorage('|') 
AS (userID:int, age:int, gender:chararray, occupation:chararray, zip:int);

STORE users INTO 'hbase://users' 
USING org.apache.pig.backend.hadoop.hbase.HBaseStorage (
'userinfo:age,userinfo:gender,userinfo:occupation,userinfo:zip');
```

```shell
pig hbase.pig
```

```shell
hbase shell
list
scan 'users'
disable 'users'
drop 'users'
exit
```

### Cassandra

* distributed non-relational database
* no master node

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%204.16.12%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%204.19.14%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%204.22.09%20PM.png?raw=true)

#### Cassandra architecture

* ring architecture
* gossip protocol
* each node is same function
* read, n of N nodes consistent

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%204.27.57%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%204.29.24%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%204.32.20%20PM.png?raw=true)

#### Installing Cassandra

```shell
maria_dev
su root
python -V # horton need python 2.6
yum update
yum install scl-utils
yum install centos-release-scl-rh
yum install python27
scl enable python27 base
python -V # 2.7
cd /etc/yum.repos.d
vi datastax.repo
[datastax]
name = DataStax Repo for Apache Cassandra
baseurl = http://rpm.datastax.com/community
enabled = 1
gpgcheck = 0

yum install dsc30
pip install cqlsh
service cassandra start
cqlsh --cqlversion="3.4.0"
CREATE KEYSPACE movielens WITH replication = {'class': 'SimpleStrategy', 'replicateion_factor':'1'} AND durable-writes = true;
USE movielens;
CREATE TABLE users (user_id int, age int, gender text, occupation text, zip text, PRIMARY KEY (user_id));
DESCRIBE TABLE users;
SELECT * FROM  users;
```

```shell
wget http://media.sundog-soft.com/hadoop/CassandraSpark.py
export SPARK_MAJOR_VERSION=2
```

```python
from pyspark.sql import SparkSession
from pyspark.sql import Row
from pyspark.sql import functions

def parseInput(line):
    fields = line.split('|')
    return Row(user_id = int(fields[0]), age = int(fields[1]), gender = fields[2], occupation = fields[3], zip = fields[4])

if __name__ == "__main__":
    # Create a SparkSession
    spark = SparkSession.builder.appName("CassandraIntegration").config("spark.cassandra.connection.host", "127.0.0.1").getOrCreate()

    # Get the raw data
    lines = spark.sparkContext.textFile("hdfs:///user/maria_dev/ml-100k/u.user")
    # Convert it to a RDD of Row objects with (userID, age, gender, occupation, zip)
    users = lines.map(parseInput)
    # Convert that to a DataFrame
    usersDataset = spark.createDataFrame(users)

    # Write it into Cassandra
    usersDataset.write\
        .format("org.apache.spark.sql.cassandra")\
        .mode('append')\
        .options(table="users", keyspace="movielens")\
        .save()

    # Read it back from Cassandra into a new Dataframe
    readUsers = spark.read\
    .format("org.apache.spark.sql.cassandra")\
    .options(table="users", keyspace="movielens")\
    .load()

    readUsers.createOrReplaceTempView("users")

    sqlDF = spark.sql("SELECT * FROM users WHERE age < 20")
    sqlDF.show()

    # Stop the session
    spark.stop()
```

```shell
spark-submit --packages datastax:spark-cassandra-connector:2.0.0-M2-s_2.11 CassandraSpark.py

cqlsh --cqlversion="3.4.0"
use movielens;
select * from users limit 10;
exit
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%204.59.15%20PM.png?raw=true)

### MongoDB

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%205.01.45%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%205.03.10%20PM.png?raw=true)

#### MongoDB terminology

* Databases
* Collections
* Documents

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%205.05.50%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%205.08.32%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%209.33.59%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%209.36.54%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%209.38.41%20PM.png?raw=true)

#### Install MongoDB, and integrate Spark with MongoDB

```shell
maria_dev
su root
cd /var/lib/ambari-server/resources/stacks
cd HDP
cd 2.5
cd services
git clone https://github.com/nikunjness/mongo-ambari.git
sudo service ambari restart
```

* amber -> Actions -> add services -> mongoDB -> next… -> deploy

```shell
pip install pymongo
```

```shell
wget http://media.sundog-soft.com/hadoop/MongoSpark.py
```

```python
from pyspark.sql import SparkSession
from pyspark.sql import Row
from pyspark.sql import functions

def parseInput(line):
    fields = line.split('|')
    return Row(user_id = int(fields[0]), age = int(fields[1]), gender = fields[2], occupation = fields[3], zip = fields[4])

if __name__ == "__main__":
    # Create a SparkSession
    spark = SparkSession.builder.appName("MongoDBIntegration").getOrCreate()

    # Get the raw data
    lines = spark.sparkContext.textFile("hdfs:///user/maria_dev/ml-100k/u.user")
    # Convert it to a RDD of Row objects with (userID, age, gender, occupation, zip)
    users = lines.map(parseInput)
    # Convert that to a DataFrame
    usersDataset = spark.createDataFrame(users)

    # Write it into MongoDB
    usersDataset.write\
        .format("com.mongodb.spark.sql.DefaultSource")\
        .option("uri","mongodb://127.0.0.1/movielens.users")\
        .mode('append')\
        .save()

    # Read it back from MongoDB into a new Dataframe
    readUsers = spark.read\
    .format("com.mongodb.spark.sql.DefaultSource")\
    .option("uri","mongodb://127.0.0.1/movielens.users")\
    .load()

    readUsers.createOrReplaceTempView("users")

    sqlDF = spark.sql("SELECT * FROM users WHERE age < 20")
    sqlDF.show()

    # Stop the session
    spark.stop()
```

```shell
export SPARK_MAJOR_VERSION=2
SPARK-SUBMIT --packages org.mongodb.spark:mongo-spark-connector_2.11:2.0.0 MongoSpark.py
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%209.59.46%20PM.png?raw=true)

```shell
mongo
use movelens
db.users.find( {user_id: 100})
db.user.explain().find( {user_id: 100}) # explain

# create index
db.user.createIndex( {user_id: 1}) # 1 ascending
# index scan now

db.users.aggregate( [
	{ $group: { _id: {occupation: "$occupation"}, avgAge: {$avg: "$age"}}}
])
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.07.58%20PM.png?raw=true)

```shell
db.users.count()
db.getCollectionInfos()
db.user.drop()
```

### Choosing a database

* integration considerations
* scaling requirements
* support considerations
* Budget
* CAP considerations 

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.17.16%20PM.png?raw=true)

* simplicity

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.19.09%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.20.28%20PM.png?raw=true)

None of above. Just use Hadoop file system and tools available

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.22.36%20PM.png?raw=true)

cassandra

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.28.01%20PM.png?raw=true)

## CH7: Query your data interactively

Query Engines:

* Dirll -> mongoDB
* Hue
* Phoenix
* presto -> cassandra
* zeppelin

### Drill

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.35.57%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.37.01%20PM.png?raw=true)

connect to TableU

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.38.28%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.40.07%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.40.46%20PM.png?raw=true)

### Setting up Drill

* amber -> login admin -> start MongoDB
* Hive view 

```sql
CREATE DATABASE movielens;
```

* upload table -> u.data -> movielens table

```shell
maria_dev
su root
export SPARK_MAJOR_VERSION=2
spark-submit --packages org.mongodb.spark:mongo-spark-connector_2.11:2.0.0 MongoSpark.py

# Install Drill
# drill.apache.org
wget <link>/apache-drill-1.9.0.tar.gz
tar -xvf apache-drill...
cd apache-dirll...
bin/drillbit.sh start -Ddrill.exec.http.port=8765 # startup drill
# 127.0.0.1:8765
```

* Storage -> update Hive -> change hive.metastore.uris

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2010.54.09%20PM.png?raw=true)

```sql
show databases;
select * from hive.movielens.ratings limit 10; # from Hive
select * from mongo.movielens.users limit 10; # from mongoDB

# combined
select u.occupation, count(*) 
from hive.movielens.ratings r 
join mongo.movielens.users u 
on r.user_id = u.user_id 
group by u.occupation;
```

```shell
bin/drillbit.sh stop
```

* ambari -> stop mongoDB

### Phoenix

sql for HBase

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2011.03.38%20PM.png?raw=true)

#### why phoenix

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2011.06.27%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2011.11.05%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-26%20at%2011.11.52%20PM.png?raw=true)

#### install phoenix and query HBase

* amber -> start HBase

```shell
maria_dev
su root
yum install phoenix
cd /usr/hdp/current/phoenix-client
cd bin
python sqlline.py

!tables; # system tables

create table if not exists us_population (
state CHAR(2) Not NULL,
city varchar not null,
population bigint
contraint my_pk primary key (state, city));

!tables # table created

# cannot insert!
upsert into us_population values ('NY', 'New Your', 823425);
upsert into us_population values ('CA', 'Los Angeles', 8234232342325);

select * from us_population;
select * from us_population where state='CA';

drop table us_population;

!quit
```

#### integrate phoenix with pig

```shell
python sqlline.py
create table users( userid integer not null, age integer, gender char(1), occupation varchar, zip varchar constraint pk primary key (userid));
!tables
!quit

cd /home/maria_dev
wget http://media.sundog-soft.com/hadoop/ml-100k/u.user
cd ..
wget http://media.sundog-soft.com/hadoop/phoenix.pig
```

```pig
REGISTER /usr/hdp/current/phoenix-client/phoenix-client.jar

users = LOAD '/user/maria_dev/ml-100k/u.user' 
USING PigStorage('|') 
AS (USERID:int, AGE:int, GENDER:chararray, OCCUPATION:chararray, ZIP:chararray);

STORE users into 'hbase://users' using
    org.apache.phoenix.pig.PhoenixHBaseStorage('localhost','-batchSize 5000');

# table, userid and occupation column
occupations = load 'hbase://table/users/USERID,OCCUPATION' using org.apache.phoenix.pig.PhoenixHBaseLoader('localhost');

grpd = GROUP occupations BY OCCUPATION; 
cnt = FOREACH grpd GENERATE group AS OCCUPATION,COUNT(occupations);
DUMP cnt;  

```

```shell
pig phoenix.pig
```

### Presto

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%2011.07.08%20AM.png?raw=true)

#### Why Presto

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%2011.10.35%20AM.png?raw=true)

#### What can Presto connect to

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%2012.19.06%20PM.png?raw=true)

#### install Preso and query Hive with it

```shell
maria_dev
su root

# prestodb.io
wget https://...
tar -xvf presto...
cd presto...

wget http://media.sundog-soft.com/hadoop/presto-hdp-config.tgz
tar -xvf presto...
```

config.properties

```shell
coordinator=true
node-scheduler.include-coordinator=true
http-server.http.port=8090
query.max-memory=10GB
query.max-memory-per-node=1GB
discovery-server.enabled=true
discovery.uri=http://127.0.0.1:8090
```

node.properties

```shell
node.environment=production
node.id=f7c4bf3c-dbb4-4807-baae-9b7e41807bc8
node.data-dir=/var/presto/data
```

hive.properties

```shell
connector.name=hive-hadoop2
hive.metastore.uri=thrift://127.0.0.1:9083
hive.config.resources=/etc/hadoop/conf/core-site.xml,/etc/hadoop/conf/hdfs-site.xml
```

command line interface

```shell
wget presto-cli-0.165-executable.jar
mv presto-cli... presto
chmod +x presto
cd ..
bin/launcher start
```

127.0.0.1:8090

```shell
bin/presto --server 127.0.0.1:8090 --catalog hive # hive 

show tables from default;
select * from default.ratings limit 10;

select * from default.ratings where rating = 5 limit 10;

select count(*) from default.ratings where rating = 1; 

quit
```

```shell
bin/launcher stop
```

#### query both cassandra and hive using presto

```shell
scl enable python27 bash
python -V
service cassandra start

nodetool enablethrift # thrift server
cqlsh --cqlversion="3.4.0"

describe keyspaces;
use movielens;
select * from users limit 10;
quit
```

```shell
cd etc/datalog
vi cassandra.properties

connector.name=cassandra
cassandra.contact-points=127.0.0.1

cd ../..
bin/launcher start
bin/presto --server 127.0.0.1:8090 --catalog hive,cassandra

show tables from cassandra.movielens;
describe cassandra.movielens.users;
select * from cassandra.movielens.users limit 10;
select * from hive.default.ratings limit 10;
select u.occupation, count(*) from hive.default.ratings r join cassandra.movielens.users u on r.user_id = u.user_id froup by u.occupation;
```

## Ch8: Managing your cluster

### hadoop yarn

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.10.14%20PM.png?raw=true)

#### where yarn fits in

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.11.31%20PM.png?raw=true)

#### how YARN works

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.16.16%20PM.png?raw=true)

### Tez

Directed Acyclic Graph framework

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.20.06%20PM.png?raw=true)

#### Directed Acyclic Graphs

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.22.06%20PM.png?raw=true)

#### Use Hive on Tez and measure the performance benefit

* amber -> Hive view -> movielens
* upload table -> u.item
* query -> see tables

```sql
DROP VIEW IF EXISTS topMovieIDs;

CREATE VIEW topMovieIDs AS
SELECT movie_id, count(movie_id) as ratingCount
FROM movielens.ratings
GROUP BY movie_id
ORDER BY ratingCount DESC;

SELECT n.name, ratingCount
FROM topMovieIDs t JOIN movielens.namesn ON t.movie_id = n.movie_id;
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.31.46%20PM.png?raw=true)

### Mesos

another resource negotiator

#### What is Mesos

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.34.59%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.36.20%20PM.png?raw=true)

Difference between Mesos and YARN

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.37.04%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.40.28%20PM.png?raw=true)

#### when to use Mesos

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.41.07%20PM.png?raw=true)

### ZOOKEEPER

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.42.06%20PM.png?raw=true)

#### Failure modes

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.45.51%20PM.png?raw=true)

#### "primitive" operations in a distributed system

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.47.18%20PM.png?raw=true)

#### ZooKeeper's API

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.48.22%20PM.png?raw=true)

#### Notifications

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.50.16%20PM.png?raw=true)

#### Persistent and ephemeral znodes

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.51.40%20PM.png?raw=true)

#### ZooKeeper Architecture

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%201.52.26%20PM.png?raw=true)

#### [Activity] Simulating a failing master with ZooKeeper

```shell
maria_dev
su root
cd /usr/hdp/current/zookeeper-client
./zkCli.sh
ls / # list all in root
create -e /testmaster "127.0.0.1:2223" # -e live with the cli
get /testmaster
quit

create -e /testmaster "127.0.0.1:2225" # can only create one
```

### Oozie

orchestrating your hadoop jobs

* a system for running and scheduling Hadoop tasks

#### workflows

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%202.05.56%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%202.06.21%20PM.png?raw=true)

XML

#### set up a workflow in Oozie

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%202.09.44%20PM.png?raw=true)

Running a workflow with Oozie

```shell
oozie job --oozie http://localhost:11000/oozie -config /home/maria_dev/job.properties -run

# Monitor porgress at http://127.0.0.1:11000/oozie
```

#### Oozie Coordinators

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%202.13.54%20PM.png?raw=true)

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%202.14.53%20PM.png?raw=true)

#### Ozzie bundle

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%202.15.16%20PM.png?raw=true)

#### Set up a simple workflow in Oozie

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%202.17.03%20PM.png?raw=true)

```shell
maria_dev
mysql -u root -p hadoop
show databases;
quit
wget http://media.sundog-soft.com/hadoop/movielens.sql

mysql -u root -p hadoop
set names 'utf8';
set character set utf8;

create database movielens;
use movielens;
source movielens.sql
show tables;
select * from movies limit 10;

grant all privileges on movielens.* to ''@'localhost';
quit

# Hive script
wget http://media.sundog-soft.com/hadoop/oldmovies.sql
```

```sql
DROP TABLE movies;
CREATE EXTERNAL TABLE movies (movie_id INT, title STRING, release DATE) 
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
LOCATION '/user/maria_dev/movies/';

INSERT OVERWRITE DIRECTORY '${OUTPUT}' 
SELECT * FROM movies 
WHERE release < '1940-01-01' 
ORDER BY release;
```

```shell
# workflow file
wget http://media.sundog-soft.com/hadoop/workflow.xml
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workflow-app
    xmlns="uri:oozie:workflow:0.2" name="old-movies">
    <start to="sqoop-node"/>
    <action name="sqoop-node">
        <sqoop
            xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <prepare>
                <delete path="${nameNode}/user/maria_dev/movies"/>
            </prepare>
            <configuration>
                <property>
                    <name>mapred.job.queue.name</name>
                    <value>${queueName}</value>
                </property>
            </configuration>
            <command>
import --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --table movies -m 1
</command>
        </sqoop>
        <ok to="hive-node"/>
        <error to="fail"/>
    </action>
    <action name="hive-node">
        <hive
            xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <prepare>
                <delete path="${nameNode}/user/maria_dev/oldmovies"/>
            </prepare>
            <configuration>
                <property>
                    <name>mapred.job.queue.name</name>
                    <value>${queueName}</value>
                </property>
            </configuration>
            <script>oldmovies.sql</script>
            <param>OUTPUT=/user/maria_dev/oldmovies</param>
        </hive>
        <ok to="end"/>
        <error to="fail"/>
    </action>
    <kill name="fail">
        <message>
Sqoop failed, error message[${wf:errorMessage(wf:lastErrorNode())}]
</message>
    </kill>
    <end name="end"/>
</workflow-app>
```

```shell
wget http://media.sundog-soft.com/hadoop/job.properties
```

```shell
nameNode=hdfs://sandbox.hortonworks.com:8020
jobTracker=http://sandbox.hortonworks.com:8050
queueName=default 
oozie.use.system.libpath=true
oozie.wf.application.path=${nameNode}/user/maria_dev
```

```shell
hadoop fs -put workflow.xml /user/maria_dev
hadoop fs -put oldmovies.sql /user/maria_dev
hadoop fs -pu /usr/share/java/mysql-connector-java.jar 
# go to ambari -> files view -> user -> oozie -> share -> lib
/user/oozie/share/lib/lib_20161025075203/sqoop
# restart Oozie
# ambari -> Oozie -> restart all

oozie job -oozie http://localhost:11000/oozie -config /home/maria_dev/job.properties -run
# get job id
# 127.0.0.1:11000/oozie

# go to files view
# /user/maria_dev/0000 file is there
```

### Zeppelin

a notebook interface 

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%203.39.29%20PM.png?raw=true)

#### spark integration

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%203.40.05%20PM.png?raw=true)

```shell
# 127.0.0.1:9995
create new note

# setting - change interpreter seq

# markdown
%md

# spark context object - sc
# spark sql object - sqlcontext
sc.verion # spark version

%sh # shell command
wget http://media.sundog-soft.com/hadoop/ml-100k/u.data -O /tmp/u.data # -O output
wget http://media.sundog-soft.com/hadoop/ml-100k/u.item -O /tmp/u.item
echo "downloaded!"

%sh
hadoop fs -rm -r -f /tmp/ml-100k # -r recursively -f force
hadoop fs -mkdir /tmp/ml-100k
hadoop fs -put /tmp/u.data /tmp/ml-100k/
hadoop fs -put /tmp/u.item /tmp/ml-100k/

# scala is primary interpreter
final case class Rating(movieID: Int, rating: Int)

val lines = sc.textFile("hdfs:///tmp/ml-100k/u.data").map(x=> {val fields = x.split("\t"); Rating(fields(1).toInt, fields(2).toInt)}) # immutable varaible

# conver to data frame
import sqlContext.implicits._
val ratingsDF = lines.toDF()
ratingsDF.printSchema()

val topMovieIDs = ratingsDF.groupBy("movieID").count().orderBy(desc("count")).cache()
topMovieIDs.show()

ratingsDF.registerTempTable("ratings")

%sql
select * from ratings limit 10

%sql
select rating, count(*) as count from ratings group by rating

final case class Movie(movieID: Int, title: String)

val lines = sc.textFile("hdfs:///tmp/ml-100k/u.item").map(x => {val fields = x.split('|'); Movie(fields(0).toInt, fields(1))})

import sqlContext.implicits._
val moviesDF = lines.toDF()
moviesDF.shwo()

moviesDF.registerTempTable("titles")

%sql
select t.title, count(*) cnt from ratings r join titles t on r.movieID = t.movieID group by t.title order by cnt desc limit 20
```

### HUE

hadoop user experience 

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%204.06.55%20PM.png?raw=true)

* Oozie editor
  * also spark, pig, hive, hbase, hfs, sqoop
* built-in notebooks

gethue.com

## CH9: Feeding Data to your Cluster

### Kafka

```shell
ambari - kafka - start

maria_dev
cd /usr/hdp/current/kafka-broker/

# create a kafka topic
./kafka-topics.sh --create --zookeeper sandbox.hortonworks.com:2181 --replication-factor 1 --partitions 1 --topic fred
# topic created

# list topics
./kafka-topics.sh --list --zookeeper sandbox.hortonworks.com:2181

# app producer app
./kafka-console-producer.sh --borker-list sandbox.hortonworks.com:6667 --topic fred

# input message
.....

# open up a second console
cd /usr/hdp/current/kafka-broker/bin
./kafka-console-consumer.sh --bootstrap-server sandbox.hotonworks.com:6667 --zookeeper localhost:2181 --topic fred --from-beginning
```

#### Publishing web logs with Kafka

```shell
# config file connector
cd conf
cp connect-standalone.properties ~/
cp connect-file-sink.properties ~/
cp connect-file-source.properties ~/
cd ~
vi connect-standalone.properties
bootstrap.servers=sandbox.hortonworks.com:6667

vi connect-file-sink.properties
file=/home/maria_dev/logout.txt
topics=log-test

vi connect-file-source.properties
file=/home/maria_dev/access_log_small.txt
topic=log-test

wget http://media.sundog-soft.com/hadoop/access_log_small.txt

# set up consumer - 2nd console
cd /usr/hdp/current/kafka-broker/bin
./kafka-console-consumer.sh --boostrap-server sandbox.hortonworks.com:6667 --topic log-test --zookeeper localhost:2181

# back to first console
cd /usr/hdp/current/kafka-broker/broker/bin
./connect-standalone.sh ~/connect-standalone.properties ~/connect-file-source.properties ~/connect-file-sink.properties
```

### FLUME

* stream data into your cluster
* built-in sinks for hdfs and hbase
* originally made to handle log aggregation

#### Flume Agent and Flow

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%205.01.24%20PM.png?raw=true)

#### Components of an agent

* source 
  * where data is coming from
  * can optionally have Channel Selectors and Interceptors
* Channel
  * How the data is transferred (via memory or files)
* Sink
  * where the data is going
  * Can be organized into Sink Groups
  * a sink can connect to only one channel
    * channel is notified to delete a message once the sink processes it.

#### built-in source types

* spooling directory
* Avro
* Kafka
* Exec
* Thrift
* Netcat
* HTTP
* Custom
* ...

#### agents can connect to other agents

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%205.06.44%20PM.png?raw=true)

Think of Flume as a buffer

#### simple flow

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%205.09.14%20PM.png?raw=true)

```shell
maria_dev
wget media.sundog-soft.com/hadoop/example.conf
```

```shell
# example.conf: A single-node Flume configuration

# Name the components on this agent
a1.sources = r1
a1.sinks = k1
a1.channels = c1

# Describe/configure the source
a1.sources.r1.type = netcat
a1.sources.r1.bind = localhost
a1.sources.r1.port = 44444

# Describe the sink
a1.sinks.k1.type = logger

# Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1
```

```shell
cd /usr/hdp/current/flume-server
bin/flume-ng agent --conf conf --conf-file ~/example.conf --name a1 -Dflume.root.logger-INFO,console

# second console
telnet localhost 44444
# messages
...
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%205.10.09%20PM.png?raw=true)

```shell
wget media.sundog-soft.com/hadoop/flumelogs.conf
```

```shell
# flumelogs.conf: A single-node Flume configuration

# Name the components on this agent
a1.sources = r1
a1.sinks = k1
a1.channels = c1

# Describe/configure the source
a1.sources.r1.type = spooldir
a1.sources.r1.spoolDir = /home/maria_dev/spool
a1.sources.r1.fileHeader = true
a1.sources.r1.interceptors = timestampInterceptor
a1.sources.r1.interceptors.timestampInterceptor.type = timestamp

# Describe the sink
a1.sinks.k1.type = hdfs
a1.sinks.k1.hdfs.path = /user/maria_dev/flume/%y-%m-%d/%H%M/%S
a1.sinks.k1.hdfs.filePrefix = events-
a1.sinks.k1.hdfs.round = true
a1.sinks.k1.hdfs.roundValue = 10
a1.sinks.k1.hdfs.roundUnit = minute

# Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1
```

```shell
mkdir spool

# ambari - files view - user - maria_dev
# new folder flume

bin/flume-ng agent --conf conf --conf-file ~/flumelogs.conf --name a1 -Dflume.root.logger-INFO,console

# second conole
cp access_log_small.txt spool/fred.txt
```

## Ch10: Analysing Streams of Data

### spark streaming

* analyze data streams in real time instead of in huge batch jobs daily

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%206.10.03%20PM.png?raw=true)

this work can be distributed

* processing of RDD's can happed in parallel on different worker nodes