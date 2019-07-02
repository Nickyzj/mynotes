Hadoop

* 离线数据分析
* 并行计算

VMware

* ESXi - VMware vSphere Hypervisor (ESXi) 6.7U2
* [VMware vSphere Hypervisor (ESXi) 6.7U2](https://my.vmware.com/en/web/vmware/info/slug/datacenter_cloud_infrastructure/vmware_vsphere/6_7)

Namenode

* HDFS 守护程序
* 记录文件如何分块
* 对内存 io 管理
* 单点

secondary namenode

* 保存 name node 元数据信息
* name node 失效后，secondary 不会自动取代

datanode

* 每台服务器都运行一个
* 负责 HDFS 数据块读写到本地文件系统

jobTracker

* 处理作业后台程序
* 监控 task，重启 task（于不通节点）
* 每个集群只有一个

taskTracker

* 位于 slave 节点，与 datanode 结合
* 每个节点只有一个 taskTracker，可启动多个 JVM，并行执行 map reduce
* 与 jobTracker 交互

Master

* namenode, secondary namenode, jobtracker

slave

* tasktracker, dataNode

**ssh keygen config**

```shell
ssh-keygen -t -rsa
ls -a # show .ssh folder
cd .ssh
id_rsa
id_rsa.pub

# then do ssh-keygen in target machine
# copy pub to target .ssh folder, named as authorized_keys
# moust be -rw-r--r--
scp ./id_rsa.pub <user>@<ip>:/<path>/authorized_keys 
```

download hadoop

