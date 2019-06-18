# [Java面试题-阿里、饿了么、链家、携程](https://zhuanlan.zhihu.com/p/66402742)

# J2SE

## Java basics

#### difference between == and equals()

* == is for value, 比较对象时比较地址
* equals()方法存在于Object类中,Object类中equals()方法底层依赖的是==操作,在所有没有重写equals()的类中，调用equals()其实和使用==的效果一样，也是比较的地址值。String重写了equals()，底层比较的是两个String对应位置的char字符是否==

##### 为什么重写equals()方法就必须重写hashCode()方法?

1. Object.hashCode()方法是一个本地native方法，返回的是对象引用中存储的对象的内存地址;

2. 基于散列的集合(HashSet、HashMap和Hashtable)存放key时，调用该对象（存入对象）的hashCode()方法来得到该对象的hashCode值，然后根据该hashCode值决定该对象在HashSet中存储的位置；

3. 所以如果equals方法返回true，那么两个对象的hasCode()返回值必须一样；

[How HashMap works in Java? With Animation!! whats new in java8 tutorial](https://www.youtube.com/watch?v=c3RVW3KGIIE)

Hashmap allows null key, which always goes to index 0 as hash of null is 0

Java8, 当不同 key 相同 hashcode 超过 TREEIFY_THRESHOLD = 8 时，该分支从 linked list 转为 balanced tree。O(n) -> O(log n)