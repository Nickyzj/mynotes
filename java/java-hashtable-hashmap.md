# [HashTable vs HashMap vs Concurrent HashMap all kinds of Map implementations](https://www.youtube.com/watch?v=APL28XpFP0c)

## java.util.HashTable

* legacy associative array implementation; inducted to collection family by implementing Map interface later
* all methods are thread-save
* there is "synchronized" keyword on each public method such as (put, get, remove)
* overhead in an environment where Map is initialized once and the read by multiple threads

## java.util.HashMap

* Map implementation 适用于大部分基本场景
* **not** thread-safe
* 顺序不保证
* 需要用"synchronized" 保证多线程安全
* 适用于一次加载数据后被多线程读取访问，没有性能问题

## java.util.LinkedHashMap

* similar to HashMap
* 保证插入顺序
* 双链表
* 适用于需要保存顺序的 HashMap

## java.util.TreeMap

* 实现 SortedMap 和 NavigableMap 接口
* 根据 key 排序
* key 需要实现 Comparable 接口，或在构造函数中提供 Comparator
* 红黑树。NavigableMap 接口提供接近(floorEntry())方法

## java.util.IdentityHashMap

* use identity to store and retrieve key values
* 使用==比较，refrence equality。使用 System.identityHashCode(givenkey) 而不是 givenKey.hashCode()
* 

## java.util.EnumMap

