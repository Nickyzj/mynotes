进程

```
jps -l
```

查看死锁

```
jstack 12464 > deadlock.txt
```

查看线程

```
top -H -p <pid>
```

看heap

```
jinfo -flag MaxHeapSize 17644
jmap -heap 15616
```

