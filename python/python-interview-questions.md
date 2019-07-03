## basic python questions

### difference between deep and shallow copy

https://www.runoob.com/w3cnote/python-understanding-dict-copy-shallow-or-deep.html

* 直接赋值：其实就是对象的引用（别名）。
* 浅拷贝(copy)：拷贝父对象，不会拷贝对象的内部的子对象。
* 深拷贝(deepcopy)： copy 模块的 deepcopy 方法，完全拷贝了父对象及其子对象。

**浅拷贝**

```python
a = {1: [1, 2, 3]}
b = a.copy()
a, b
({1: [1, 2, 3]}, {1: [1, 2, 3]})
a[1].append(4)
a, b
({1: [1, 2, 3, 4]}, {1: [1, 2, 3, 4]})
```

**深度拷贝需要引入 copy 模块**

```python
import copy
c = copy.deepcopy(a)
a, c
({1: [1, 2, 3, 4]}, {1: [1, 2, 3, 4]})
a[1].append(5)
({1: [1, 2, 3, 4, 5]}, {1, [1, 2, 3, 4]})
```



**id() 函数用于获取对象的内存地址**。

```python
>>>a = 'runoob'
>>> id(a)
4531887632
>>> b = 1
>>> id(b)
140588731085608
```

### List and tuples

```python
l1 = [1, 2, 3, 4] # mutable
t1 = (1, 2, 3, 4) # immutable
t2 = ([1, 2, 3], ) # t2[0] mutable
```

### multi-threading

* GIL (Global Interpreter Lock) makes sure only one "threads" can execute at any time.

* A thread acquries GIL, does a little work, then passes GIL onto next thread

  