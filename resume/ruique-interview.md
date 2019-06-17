<https://www.job592.com/pay/ms/d47069021.html>

<https://hlwhr.ofweek.com/jobs/jobs-show-2183572.html>

### 职责描述

1. 参与公司产品的需求分析，深入了解软件需求说明书，找出系统设计阶段存在的问题及缺陷，对产品提出进一步改进的建议，并评估改进方案是否合理。

2. 根据测试流程及规范，制定测试计划、编写测试用例和脚本。

3. 负责公司所有系统的接口测试、功能测试、集成测试及性能测试。

4. 编写测试报告，对测试结果进行总结与统计分析，并给出有价值的改善意见和建议。

5. 收集软件研发过程中存在的风险，并及时反馈。

6. 为业务部门提供相应技术支持，确保软件质量指标。

7. 测试工具/系统的研究和应用。


## 任职资格

1. 计算机相关专业专科以上学历,有5到10年测试经验；其中3年以上自动化测试经验。
2. 熟悉基本的软件测试流程，方法和规范，能编写测试计划，测试用例和测试报告；
3. 熟练掌握自动化测试工具Selenium，有自动化测试框架设计经验；
4. 熟练使用常用的测试管理工具：mantis、JIRA、TestLink等；
5. 熟练使用至少一种配置管理工具：SVN、GIT等；
6. 熟悉数据库操作，使用过Oracle，SQLServer、Mysql任意一种数据库
7. 熟悉常用脚本语言：Python、Shell、Ruby者优先考虑；熟悉java,C#,C++者优先考虑；
8. 较强的逻辑思维能力、分析能力和定位问题的能力，工作态度认真严谨，做事积极主动，有较强责任心。



## 面试

1. java基础，多线程，

2. linux等的问题，

3. 当前的自动化框架是怎么搭建的，遇到了些什么问题，

   [How to build an agile-friendly test automation framework](<https://techbeacon.com/app-dev-testing/how-build-agile-friendly-test-automation-framework>)

4. 一些简单算法题，

5. devops，

6. 微服务，

7. 测试基础等 

面试官问的面试题：



1. python去除重复字符串，要求起码说出三种方式

   ```python
   >>> t = [1, 2, 3, 1, 2, 5, 6, 7, 8]
   >>> t
   [1, 2, 3, 1, 2, 5, 6, 7, 8]
   >>> list(set(t))
   [1, 2, 3, 5, 6, 7, 8]
   >>> s = [1, 2, 3]
   >>> list(set(t) - set(s))
   [8, 5, 6, 7]
   
   >>> from collections import OrderedDict
   >>> list(OrderedDict.fromkeys(t))
   [1, 2, 3, 5, 6, 7, 8]
   
   In Python 3.7, the regular dict is guaranteed to both ordered across all implementations. So, the shortest and fastest solution is:
   
   >>> list(dict.fromkeys('abracadabra'))
   ['a', 'b', 'r', 'c', 'd']
   
   >>> t = [1, 2, 3, 1, 2, 5, 6, 7, 8]
   >>> t
   [1, 2, 3, 1, 2, 5, 6, 7, 8]
   >>> s = []
   >>> for i in t:
          if i not in s:
             s.append(i)
   >>> s
   [1, 2, 3, 5, 6, 7, 8]
   ```

   

2. 怎么样实现两个json的比对

   ```python
   To fix that, we can define an ordered function which will recursively sort any lists it finds (and convert dictionaries to lists of (key, value) pairs so that they're orderable):
                                                                                         
   def ordered(obj):
       if isinstance(obj, dict):
           return sorted((k, ordered(v)) for k, v in obj.items())
       if isinstance(obj, list):
           return sorted(ordered(x) for x in obj)
       else:
           return obj
       
   >>> ordered(a) == ordered(b)
   True
   ```



```python
Python sorted() 函数

sort 与 sorted 区别：

sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作。

list 的 sort 方法返回的是对已经存在的列表进行操作，无返回值，而内建函数 sorted 方法返回的是一个新的 list，而不是在原来的基础上进行的操作。

>>>a = [5,7,6,3,4,1,2]
>>> b = sorted(a)       # 保留原列表
>>> a 
[5, 7, 6, 3, 4, 1, 2]
>>> b
[1, 2, 3, 4, 5, 6, 7]
 
>>> L=[('b',2),('a',1),('c',3),('d',4)]
>>> sorted(L, cmp=lambda x,y:cmp(x[1],y[1]))   # 利用cmp函数
[('a', 1), ('b', 2), ('c', 3), ('d', 4)]
>>> sorted(L, key=lambda x:x[1])               # 利用key
[('a', 1), ('b', 2), ('c', 3), ('d', 4)]
 
 
>>> students = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
>>> sorted(students, key=lambda s: s[2])            # 按年龄排序
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
 
>>> sorted(students, key=lambda s: s[2], reverse=True)       # 按降序
[('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
```



1. set， map ， json的区别

   [Python Set](<https://www.datacamp.com/community/tutorials/sets-in-python>)

   

2. 给定一个random函数，只返回0，1，怎么样只用这个给定函数返回4位小数的随机数

3. 根据你写的这个函数如果做测试。

4. 给定一个登录页面，设计测试用例 





## 公司简介

上海瑞阙文化发展有限公司所属行业： [互联网/电子商务](http://hlwhr.ofweek.com/)   
公司地址：黄浦区新天地复兴广场A座2305(邮编：200001)

上海瑞阙文化是做交易系统研发的软件科技公司。主营内容为交易系统，让交易更简单高效安全合规，带来“纽交所”级别的交易体验。无论您的平台需要开展竞价撮合交易、应价谈判交易、大宗交易，还是场外交易和黑池交易，甚至拍卖和标准的批量权益转让，我们的交易系统都可以完美支持。互联网化和创新意识可为您的平台客户带来持续性的良好体验。

我们的团队

我们的团队主力为80后和90后，特点：年轻、激情、高效、技术牛。
我们的核心团队有来自美国的技术专家、有来自世界500强的技术总监和产品经理
还有来自五湖四海但有共同的目标孕育着同一个理想，出发点不同但目的地一样
“成为行业内的领先者和弄潮儿”的超强团队。

我们的管理
开放、透明、平等、简单，同事间工作氛围很棒，没有繁琐的工作流程。
公司将为符合要求的相关人才提供良好的发展平台和自我提升机会。

我们的希望
每一个都能人尽其才的发挥自己的才能，我们希望每个人都在做着自己挚爱的事情
充满斗志，充满热爱与激情。

您想走在世界最前端，您想学习和提升自己我们是最好的选择，我们欢迎这样的有志之士的加入!

公司网址：www.bijietech.com  



