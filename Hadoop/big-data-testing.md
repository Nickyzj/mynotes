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

