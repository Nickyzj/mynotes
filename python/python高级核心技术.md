## 2-2 type、object和class之间的关系

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/20180823172136260.png?raw=true)

**一切类都是type的实例 ，一切都继承object类**



## 3-3 [python魔法函数一览](https://pyzh.readthedocs.io/en/latest/python-magic-methods-guide.html)

## 4-4 isinstance和type的区别

若第二个参数只有一个单独的类型，对象的类型与参数二的类型相同则返回True；
若第二个参数为一个元组类型，则若对象类型与元组中类型名之一相同即返回True。

```python
>>> a = 4
>>> isinstance (a,int)
True
>>> isinstance (a,str)
False
>>> isinstance (a,(str,int,list))#与元组类型之一相同
True
>>> isinstance(a,(str,list,float))#与元组类型都不相同
False
```

**当第二个参数是class时**

```
class A(object):
    pass
>>>a=A()
>>>isinstance(a,A)
True
```

type只接收一个参数，不但可以判断变量是否属于某个类型，而且可以得到参数变量未知的所属的类型；而isinstance只能判断是否属于某个已知类型，不能直接得到变量未知的所属的类型

```
class A(object):
    pass
>>>a=A()
#type判断变量是否属于某个类型
>>>type(a)==A
True
#type得到变量类型
>>>type(a)
 __main__.A
#isinstance只能判断变量是否属于某个类型
>>>isinstance(a,A)
True
```

isinstance可以判断子类实例对象是属于父类的；而type会判断子类实例对象和父类类型不一样

```
class father(object):
    pass
class son(father):
    pass
>>>a=father()
>>>b=son()
>>>isinstance(a,father)
True
>>>type(a)==father
True
>>>isinstance(b,father)#isinstance得到子类实例是属于父类的
True
>>>type(b)==father#type对于子类实例判断不属于父类
 False
```

## 4-5 类变量和实例变量

* Python类中定义的变量分为类变量和实例变量（也叫成员变量、对象变量）
* 类变量直接定义在类里面（不在函数里面），前面不会有一个self修饰；
* 相反，实例变量大都定义在实例函数里面，通过“self.变量名”的方式进行定义。
* 例外，类变量和实例变量都可以在类定义之后在定义
* 类变量可以通过“类名.类变量名”、“实例名.类变量名”两种方式读取，即类和实例都能读取类变量。
* 实例变量只能通过“实例名.实例变量名”的方式访问，类无权访问实例名。
* “类名.类变量名”、“实例名.类变量名”访问的实际上是同一个命名空间的变量，所以类变量具有“一改全改”的特点
* **采用‘实例名.类变量名’的方式对类变量进行赋值时**，若该类变量是可变数据类型，则可以成功赋值该类变量，否则会在该实例变量所在的名称空间中创建一个与该类变量同名的实例变量进行赋值，并不会对类变量进行赋值，此时也无法再通过‘实例名.类变量名’的方式读取该类变量。但若‘实例名.类变量名’赋值的是可变数据类型，则可以对类变量进行赋值操作。



## 4-7 类方法、静态方法和实例方法

普通实例方法，第一个参数需要是self，它表示一个具体的实例本身。
如果用了staticmethod，那么就可以无视这个self，而将这个方法当成一个普通的函数使用。
而对于classmethod，它的第一个参数不是self，是cls，它表示这个类本身。

```python
# coding:utf-8
class Foo(object):
    """类三种方法语法形式"""
 
    def instance_method(self):
        print("是类{}的实例方法，只能被实例对象调用".format(Foo))
 
    @staticmethod
    def static_method():
        print("是静态方法")
 
    @classmethod
    def class_method(cls):
        print("是类方法")
 
foo = Foo()
foo.instance_method()
foo.static_method()
foo.class_method()
print('----------------')
Foo.static_method()
```

**类方法用在模拟java定义多个构造函数的情况**

```python
class Book(object):
 
    def __init__(self, title):
        self.title = title
 
    @classmethod
    def class_method_create(cls, title):
        book = cls(title=title)
        return book
 
    @staticmethod
    def static_method_create(title):
        book= Book(title)
        return book
 
book1 = Book("use instance_method_create book instance")
book2 = Book.class_method_create("use class_method_create book instance")
book3 = Book.static_method_create("use static_method_create book instance")
print(book1.title)
print(book2.title)
print(book3.title)
```

静态方法每次都要写上类的名字

**类中静态方法方法调用静态方法和类方法调用静态方法例子**

```python
class Foo(object):
    X = 1
    Y = 2
 
    @staticmethod
    def averag(*mixes):
        return sum(mixes) / len(mixes)
 
    @staticmethod
    def static_method():  # 在静态方法中调用静态方法
        print "在静态方法中调用静态方法"
        return Foo.averag(Foo.X, Foo.Y)
 
    @classmethod
    def class_method(cls):  # 在类方法中使用静态方法
        print "在类方法中使用静态方法"
        return cls.averag(cls.X, cls.Y)
 
foo = Foo()
print(foo.static_method())
print(foo.class_method())
```

**继承类中的区别**

## 4-8 数据封装和私有属性

```python
#1.通过自定义get,set方法，调用方法的形式去对私有属性进行操作
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.__age = age
 
    #定义对私有属性的get方法，获取私有属性
    def getAge(self):
        return self.__age
 
    #定义对私有属性的重新赋值的set方法，重置私有属性
    def setAge(self,age):
        self.__age = age
 
person1 = Person("tom",19)
person1.setAge(20)
print(person1.name,person1.getAge())  #tom 20
 
#2.通过调用property属性对set,get方法进行了封装。然后操作私有属性
class Student(object):
    def __init__(self, name, age):
        self.name = name
        self.__age = age
 
    #定义对私有属性的get方法，获取私有属性
    def getAge(self):
        return self.__age
 
    #定义对私有属性的重新赋值的set方法，重置私有属性
    def setAge(self,age):
        self.__age = age
 
    p = property(getAge,setAge) #注意里面getAge,setAge不能带()
 
s1 = Student("jack",22)
s1.p = 23 #如果使用=,则会判断为赋值，调用setAge方法。
print(s1.name,s1.p)  #jack 23   ，直接使用s1.p会自动判断会取值，调用getAge
print(s1.name,s1.getAge()) #jack 23,这个时候set,get方法可以单独使用。
 
#3.上面两种还是太麻烦，直接使用property标注同名函数的形式。这是最终开发中常用的方法。
class Teacher(object):
    def __init__(self, name, age,speak):
        self.name = name
        self.__age = age
        self.__speak = speak
 
 
    @property      #注意1.@proterty下面默认跟的是get方法，如果设置成set会报错。
    def age(self):
        return self.__age
 
    @age.setter    #注意2.这里是使用的上面函数名.setter，不是property.setter.
    def age(self,age):
        if age > 150 and age <=0:  #还可以在setter方法里增加判断条件
            print("年龄输入有误")
        else:
            self.__age = age
 
    @property
    def for_speak(self):  #注意2.这个同名函数名可以自定义名称，一般都是默认使用属性名。
        return self.__speak
 
    @for_speak.setter
    def for_speak(self, speak):
        self.__speak = speak
 
t1 = Teacher("herry",45,"Chinese")
t1.age = 38    #注意4.有了property后，直接使用t1.age,而不是t1.age()方法了。
t1.for_speak = "English"  
 
print(t1.name,t1.age,t1.for_speak)  #herry 38 English
```

## 4-9 python对象的自省机制

##### dir()

可以使用内置的 `dir()` 函数来检查模块（以及其它对象）的内容

`hasattr`
`setattr`
`getattr`
`delattr`

```
class A(object):
    
    def __init__(self):
        self.name = "hello"  
        
    def say(self):
        print("say {}".format(self.name))
        
a = A()
hasattr(a, 'name') # 注意： 必须是字符串的 name
>>>True
hasattr(a, 'say')
>>>True
getattr(a, 'name')
>>>'hello'
getattr(a, 'say')
>>><bound method A.say of <A object at 0x10e47a6d8>>
setattr(a, 'name', 'world')
a.name
>>>'world'
getattr(a, 'say')()
>>>say world
delattr(a, 'name')
a.name
>>>Traceback (most recent call last):
  File "/Library/Frameworks/Python.framework/Versions/3.5/lib/python3.5/code.py", line 91, in runcode
    exec(code, self.locals)
  File "<input>", line 1, in <module>
AttributeError: 'A' object has no attribute 'name'

delattr(a, 'say') #注意 不能删除实例方法
>>>Traceback (most recent call last):
  File "/Library/Frameworks/Python.framework/Versions/3.5/lib/python3.5/code.py", line 91, in runcode
    exec(code, self.locals)
  File "<input>", line 1, in <module>
AttributeError: say
```

```
class A(object):
    
    def __init__(self):
        self.name = "hello"  
        
    def say(self):
        print("say {}".format(self.name))
        
    def index(self):
        if hasattr(self, 'render'):
            render = getattr(self, 'render')
            return render('index.html')
        else:
            return '404.html'
        
a = A()
a.index()
>>>'404.html'

a.render = lambda d: d
a.index()
>>>'index.html'
```

## 4-10 super真的是调用父类吗？

**不要一说到 super 就想到父类！super 指的是 MRO 中的下一个类！**

```python
class Root(object):
  def __init__(self):
    print("this is Root")

class B(Root):
  def __init__(self):
    print("enter B")
    # print(self) # this will print <__main__.D object at 0x...>
    super(B, self).__init__()
    print("leave B")

class C(Root):
  def __init__(self):
    print("enter C")
    super(C, self).__init__()
    print("leave C")

class D(B, C):
  pass

d = D()

print(d.__class__.__mro__)

enter B
enter C
this is Root
leave C
leave B
(<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__m
```

在 B 的 init 函数中：

`super(B, self).__init__()`
首先，我们获取 self.class.mro，注意这里的 self 是 D 的 instance 而不是 B 的

然后，通过 B 来定位 MRO 中的 index，并找到下一个。显然 B 的下一个是 C。于是，我们调用 C 的 init，打出 enter C。

为什么 B 的 init 会被调用：因为 D 没有定义 init，所以会在 MRO 中找下一个类，去查看它有没有定义 init，也就是去调用 B 的 init。

## 4-12 python中的with语句

**with 工作原理**

（１）紧跟with后面的语句被求值后，返回对象的“–enter–()”方法被调用，这个方法的返回值将被赋值给as后面的变量； 
（２）当with后面的代码块全部被执行完之后，将调用前面返回对象的“–exit–()”方法。 
with工作原理代码示例：

```
class Sample:
    def __enter__(self):
        print "in __enter__"
        return "Foo"
    def __exit__(self, exc_type, exc_val, exc_tb):
        print "in __exit__"
def get_sample():
    return Sample()
with get_sample() as sample:
    print "Sample: ", sample
```

整个运行过程如下： 
（１）**enter**()方法被执行； 
（２）**enter**()方法的返回值，在这个例子中是”Foo”，赋值给变量sample； 
（３）执行代码块，打印sample变量的值为”Foo”； 
（４）**exit**()方法被调用；

【注：】**exit**()方法中有３个参数， exc_type, exc_val, exc_tb，这些参数在异常处理中相当有用。 
exc_type：　错误的类型 
exc_val：　错误类型对应的值 
exc_tb：　代码中错误发生的位置 

在with后面的代码块抛出异常时，**exit**()方法被执行。开发库时，清理资源，关闭文件等操作，都可以放在**exit**()方法中

## 4-13 contextlib简化上下文管理器

## 5-1 python中的序列分类

https://www.cnblogs.com/yyds/p/6123692.html

## 5-3 list中extend方法区别

Lists 的两个方法 extend 和 append 看起来类似，但实际上完全不同。extend 接受一个参数，这个参数总是一个 list，并且把这个 list 中的每个元素添加到原 list 中。

**·** 在这里 list 中有 3 个元素 (‘a’、’b’ 和 ‘c’)，并且使用另一个有 3 个元素 (‘d’、’e’ 和 ‘f’) 的 list 扩展之，因此新的 list 中有 6 个元素。

**·** 另一方面，append 接受一个参数，这个参数可以是任何数据类型，并且简单地追加到 list 的尾部。在这里使用一个含有 3 个元素的 list 参数调用 append 方法。

**·** 原来包含 3 个元素的 list 现在包含 4 个元素。为什么是 4 个元素呢？因为刚刚追加的最后一个元素本身是个 list。List 可以包含任何类型的数据，也包括其他的 list。这或许是您所要的结果，或许不是。如果您的意图是 extend，请不要使用 append。

## 5-4 实现可切片的对象

https://yq.aliyun.com/articles/682803/

## 5-5 bisect维护已排序序列

## 5-7 列表推导式、生成器表达式、字典推导式

https://blog.csdn.net/yjk13703623757/article/details/79490476

## 6-2 dict的常用方法

https://blog.csdn.net/JHTSunshine/article/details/58085120

## 6-4 set和frozenset

https://blog.csdn.net/lilong117194/article/details/78522459

## 6-5 dict和set的实现原理

https://blog.csdn.net/siyue0211/article/details/80560783

https://blog.csdn.net/zhao_crystal/article/details/82620524

## 7-2 ==和is的区别

https://juejin.im/entry/5a3b62446fb9a0451f311b5c

## 7-3 del语句和垃圾回收

[https://docs.lvrui.io/2018/08/01/Python%E4%B8%AD%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6%E5%92%8Cdel%E8%AF%AD%E5%8F%A5/](https://docs.lvrui.io/2018/08/01/Python中垃圾回收和del语句/)

## 8-3 属性描述符和属性查找过程

http://www.manongjc.com/article/72096.html

## 8-4 __new__和__init__的区别

https://juejin.im/post/5add4446f265da0b8d4186af

## 9-6 生成器如何读取大文件

```py
def read_large_file(file_handler, block_size=10000):
    block = []
    for line in file_handler
        block.append(line)
        if len(block) == block_size:
            yield block
            block = []

    # don't forget to yield the last block
    if block:
        yield block

with open(path) as file_handler:
    for block in read_large_file(file_handler):
        print(block)
```

## 11-1 python 中的 GIL

https://zhuanlan.zhihu.com/p/20953544

## 11-3 线程间通信 - 共享变量和 Queue

https://www.cnblogs.com/liubiao/p/6772873.html

## 11-7 ThreadPoolExecutor线程池

https://blog.csdn.net/wudiazu/article/details/80925692

https://zhuanlan.zhihu.com/p/65638744