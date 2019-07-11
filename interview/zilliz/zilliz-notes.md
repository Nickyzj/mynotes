https://www.bilibili.com/video/av37256591/?p=20

## AVL Trees

### what is a binary search tree

左边都比节点小，右边都比节点大

时间复杂度取决于高度

没有重复值

时间复杂度：logN - N

### drawback of bst

### how bst can be improved

### what is an avl tree

左边和右边高度差小于等于1

### rotations in avl tree

### how to create avl tree

## Red Black Tree

- every node is red or black
- root is always black
- new insertions are always red
- every path from root - leaf has the same number of black nodes
- no path can have two consecutive red nodes
- nulls are black



black aunt -> rotate

black - red - red

red aunt -> color flip

red - black - black

## Python二分查找算法

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# @Author  : xiaoke


def binary_search(alist, item):
    """二分查找 非递归方式"""
    n = len(alist)
    start = 0
    end = n - 1
    while start <= end:
        mid = (start + end) // 2
        if alist[mid] == item:
            return True
        elif item < alist[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return False


def binary_search_2(alist, item):
    """二分查找 递归方式"""
    n = len(alist)
    if 0 == n:
        return False
    mid = n // 2
    if alist[mid] == item:
        return True
    elif item < alist[mid]:
        return binary_search_2(alist[:mid], item)
    else:
        return binary_search_2(alist[mid + 1:], item)


if __name__ == '__main__':
    li = [17, 20, 26, 31, 44, 54, 55, 77, 93]
    # print(binary_search(li, 55))
    # print(binary_search(li, 100))
    print(binary_search_2(li, 55))
    print(binary_search_2(li, 100))
```

最优时间复杂度：O(1) 
最坏时间复杂度：O(logn)

## 删除单向链表中的某个节点

算法解释：

因为没有当前传入节点的上一个节点，因此，需要想一个折中的办法，由于上一个节点知道它的下一个节点就是当前传入的节点，因此我们将当前节点中的所有信息换成当前节点的下一个节点的信息，也就变相的完成了节点的删除。

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void deleteNode(ListNode node) {
        if (node == null)
            return;
        ListNode nextNode = node.next;
        if (nextNode == null)
            return;
        node.next = nextNode.next;
        node.val = nextNode.val;
    }
}
```

## 单链表反转的递归方法和非递归方法

**一、递归方法**先反转后面的链表，从最后面的两个结点开始反转，依次向前，将后一个链表结点指向前一个结点，注意每次反转后要将原链表中前一个结点的指针域置空，表示将原链表中前一个结点指向后一个结点的指向关系断开。

**二、非递归方法**

利用两个结点指针和一个中间结点指针temp(用来记录当前结点的下一个节点的位置)，分别指向当前结点和前一个结点，每次循环让当前结点的指针域指向前一个结点即可，翻转结束后，记得将最后一个节点的链域置为空。

## python

### 多线程

* 共享全局变量

```python
import threading
lock = threading.Lock()
with lock:
  ....
  
等价于
lock.acquire()
lock.release()

mutex = threading.Lock()
mutex.acquire()
mutex.release()
```

### 多进程

```python
import multiprocessing

p1 = multiprocessing.Process(target = fun)
p1.start()
ps -aux 显示进程
kill pid

# 多进程锁
lock = multiprocessing.Lock()
lock.acquire()
lock.release()

# RLock()
lock = threading.RLock()
lock.acquire()
lock.acquire()

```

### 进程间通讯

```python
from multiprocessing import Queue
q = Queue(3)
q.put('message') # 满了则堵塞
q.full() # True, False
q.empty()

if not q.full():
  q.put_nowait('message') # 满了抛异常
  
if not q.empty():
  for i in range(q.size()):
    print(q.get_nowait()) # 空则抛异常 Empty

q.size()
```

### 进程池

```python
from multiprocessing import Pool

p = Pool(3)

for in in range(0, 10): # 任务满了不失败，等待
  p.apply_async(fun, (param, ))
  
p.close() # 关闭进程池，不接收新请求
p.join() # 等待子进程完成，必须在 close 后
# 主进程不等待进程池中的任务，用 join 等待
```

### 进程池 queue

```python
from multiprocessing import Manager()
q = Manager().Queue()
```

### 进度条打印

```python
print("\r xxxxx %.2f %%" % (num*100/all_num), end = "")
```

