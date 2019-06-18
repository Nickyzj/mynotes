# [Garbage collection in Java, with Animation and discussion of G1 GC](https://www.youtube.com/watch?v=UnaNQgzw4zY)

## Before Java

* malloc() / realloc() / calloc()
* free()
* new and destructors

## Garbage collection

java provides automatec memory management through a program called **Garbage collector**

* **live object** = reachable (referenced by someone else)
* **dead object** = unreachable (not referenced from anywhere)

## Before we start

* Objects are allocated in **heap**, static members, class definitions(metadata), are stored in **method area**

* barbage collection is carried out by a daemon thread called **garbage collector**
* we can **not** force tc to happen (System.gc())
* when new allocations can not happen due to a full heap you got **java.lang.OutOfMemoryError**

## garbage collection three steps

### mark

starts from root node of you application (main), walks the object graph, marks objects that are reachable as live

### delete/sweep

delete unreachable objects

### compacting

compact the memory by moving around the objects and making the allocation contiguous than fragmented.

## Generational collectors

### Young Generation

* Eden space
* survivor space from
* survivor to

-XX:MaxTenuringThreshold 存活超过次数则移入 old generation

### Old(Tenured) generation

## Performance

### Responsiveness/latency

For app that focus on responsiveness, large pause times are not acceptable. the focus is on responding in short periods of time

### Throughput

focuses on maximizing the amount of work by app in a specific period of time.

high pause times are acceptable for app that focus on throughput. Over long periods of time, quick response time is not a consideration.

## Garbage collectors

* serial collector

  basic garbage collector that runs in single thread, can be used for baisc app

* concurrent collector

  a thread that performs GC along with app exec as the app runs, does not wait for old generation to be full - stops the world only during mark/re-mark

* parallel collector

  use multiple CPU to perform GC. multiple theads doing mark/sweep. does not kick in until heap is full/near-full. stops the world when it runs

### Use concurrent collector (CMS) when

* there is more memory
* there is high number of cpus
* app demands short pauses

### Use parallel collector when

* there is less memeory
* there is less number of cpu
* app demands high throughput and can withstand pauses

### G1 garbage collector 

latest entry (1.7)

* divide heap into different regions. 
* during a GC it can collect a sub-set of regions
* dynamically select a set of region to act as young generation in next gc cycle
* regions with most garbage (unreachable) will be collected first

-

* more predictable(tunable) GC pauses
* low pauses with fragmentation
* parallelism and concurrency together
* better heap utilization