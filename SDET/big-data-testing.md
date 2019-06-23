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

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/2019-06-23_172020.png?raw=true)

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