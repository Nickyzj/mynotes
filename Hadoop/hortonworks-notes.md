ssh login

* maria_dev

123

* root

hadoop

* web ssh port 

4200

* ambari port

8080, 1080(nat)

[Hive 3](https://cloudvane.net/2019/05/08/hive-tutorial-3-working-with-databases/)

[Data Analytics Studio](http://10.0.0.21:30800/)

10.0.0.21

[Web ssh](http://10.0.0.21:4200/)

```shell
ssh maria_dev@10.0.0.21 -p 2222 # maria_dev
```



http://media.sundog-soft.com/hadoop/RatingsBreakdown.py

```shell
scp -P 2222 u.data maria_dev@10.0.0.21:/home/maria_dev 
```

```shell
$ python RatingsBreakdown.py -r hadoop --hadoop-streaming-jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar u.data 
No configs found; falling back on auto-configuration
No configs specified for hadoop runner
Looking for hadoop binary in $PATH...
Found hadoop binary: /usr/bin/hadoop
Using Hadoop version 3.1.1.3.0.1.0
Creating temp directory /tmp/RatingsBreakdown.maria_dev.20190628.084909.395864
uploading working dir files to hdfs:///user/maria_dev/tmp/mrjob/RatingsBreakdown.maria_dev.20190628.084909.395864/files/wd...
Copying other local files to hdfs:///user/maria_dev/tmp/mrjob/RatingsBreakdown.maria_dev.20190628.084909.395864/files/
Running step 1 of 1...
  packageJobJar: [] [/usr/hdp/3.0.1.0-187/hadoop-mapreduce/hadoop-streaming-3.1.1.3.0.1.0-187.jar] /tmp/streamjob5612977569238113785.jar tmpDir=null
  Connecting to ResourceManager at sandbox-hdp.hortonworks.com/172.18.0.2:8050
  Connecting to Application History server at sandbox-hdp.hortonworks.com/172.18.0.2:10200
  Connecting to ResourceManager at sandbox-hdp.hortonworks.com/172.18.0.2:8050
  Connecting to Application History server at sandbox-hdp.hortonworks.com/172.18.0.2:10200
  Disabling Erasure Coding for path: /user/maria_dev/.staging/job_1561707230422_0002
  Total input files to process : 1
  number of splits:2
  Submitting tokens for job: job_1561707230422_0002
  Executing with tokens: []
  found resource resource-types.xml at file:/etc/hadoop/3.0.1.0-187/0/resource-types.xml
  Submitted application application_1561707230422_0002
  The url to track the job: http://sandbox-hdp.hortonworks.com:8088/proxy/application_1561707230422_0002/
  Running job: job_1561707230422_0002
  Job job_1561707230422_0002 running in uber mode : false
   map 0% reduce 0%
   map 100% reduce 0%
   map 100% reduce 100%
  Job job_1561707230422_0002 completed successfully
  Output directory: hdfs:///user/maria_dev/tmp/mrjob/RatingsBreakdown.maria_dev.20190628.084909.395864/output
Counters: 53
	File Input Format Counters 
		Bytes Read=2038163
	File Output Format Counters 
		Bytes Written=49
	File System Counters
		FILE: Number of bytes read=800006
		FILE: Number of bytes written=2318481
		FILE: Number of large read operations=0
		FILE: Number of read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=2038521
		HDFS: Number of bytes written=49
		HDFS: Number of large read operations=0
		HDFS: Number of read operations=11
		HDFS: Number of write operations=2
	Job Counters 
		Data-local map tasks=2
		Launched map tasks=2
		Launched reduce tasks=1
		Total megabyte-milliseconds taken by all map tasks=65488896
		Total megabyte-milliseconds taken by all reduce tasks=5495808
		Total time spent by all map tasks (ms)=63954
		Total time spent by all maps in occupied slots (ms)=255816
		Total time spent by all reduce tasks (ms)=5367
		Total time spent by all reduces in occupied slots (ms)=21468
		Total vcore-milliseconds taken by all map tasks=63954
		Total vcore-milliseconds taken by all reduce tasks=5367
	Map-Reduce Framework
		CPU time spent (ms)=6070
		Combine input records=0
		Combine output records=0
		Failed Shuffles=0
		GC time elapsed (ms)=463
		Input split bytes=358
		Map input records=100000
		Map output bytes=600000
		Map output materialized bytes=800012
		Map output records=100000
		Merged Map outputs=2
		Peak Map Physical memory (bytes)=759504896
		Peak Map Virtual memory (bytes)=2840621056
		Peak Reduce Physical memory (bytes)=222482432
		Peak Reduce Virtual memory (bytes)=2647379968
		Physical memory (bytes) snapshot=1740513280
		Reduce input groups=5
		Reduce input records=100000
		Reduce output records=5
		Reduce shuffle bytes=800012
		Shuffled Maps =2
		Spilled Records=200000
		Total committed heap usage (bytes)=1596456960
		Virtual memory (bytes) snapshot=8327454720
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
job output is in hdfs:///user/maria_dev/tmp/mrjob/RatingsBreakdown.maria_dev.20190628.084909.395864/output
Streaming final output from hdfs:///user/maria_dev/tmp/mrjob/RatingsBreakdown.maria_dev.20190628.084909.395864/output...
"1"	6110
"2"	11370
"3"	27145
"4"	34174
"5"	21201
Removing HDFS temp directory hdfs:///user/maria_dev/tmp/mrjob/RatingsBreakdown.maria_dev.20190628.084909.395864...
Removing temp directory /tmp/RatingsBreakdown.maria_dev.20190628.084909.395864...
```

