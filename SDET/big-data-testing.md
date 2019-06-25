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

