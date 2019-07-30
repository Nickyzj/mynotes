## 自我介绍

* 从事软件测试工作有10年以上经验
* 目前担任助理测试经理职位，测试开发组的 leader
* 主要负责自动化测试和性能测试和接口测试等
* 在过去的工作经历中，曾带领测试组参与多个大型项目的测试工作
* 对测试流程，测试管理，测试方法等都有较深的实践和体会
* 经过多年的学习和实践，精通 UFT，Loadrunner 等自动化测试和压力测试工具
* 对各类开源测试工具和框架也有研究和实战经验
* 也有开发测试工具，测试服务器的能力
* 编程语言熟悉 python，java
*  除了测试工作，最近有开发一个数据仓库的监控及修复系统。
* 对大数据系统，Hadoop有一定研究

## 介绍项目

### 数据仓库处理链监控及修复系统

- 背景
  - SAP 数据仓库
  - 每天处理上亿条数据，1万+个步骤，
  - 数据错误，系统错误，报警多
  - 人工检查报警响应慢，影响后续处理步骤。定位问题步骤繁琐，ops team 无法顾及
- 目标
  - 建立监控系统，展示异常信息，提供一键快速修复功能。减少工作量。
- 负责设计开发
  - 最终目标手机端接收报警，一键修复，或通知 BI team 修复
  - 设计了后台数据连接模块，前台数据展示操作模块，先电脑，后 app
  - 报警监控，问题快速修复，日志

- 异步数据传输模块
  - SAP 数据源到监控系统，前台 ajax 刷新数据
  - python 多线程，连接多个后台系统。
  - python 多线程，数据修复
  - 后台快速配置（面向对象设计，后台为一个类，各自有配置，命令队列，消息队列）
- 测试模块
  - jenkins，selenium，python， 测页面
  - jmeter，测接口

### 北美 SAP 系统联合测试

* 背景 - 全业务流程性能测试
  * 询价系统，产品询价流程 -》下订单
  * SAP ECC -》订单生成 -》生成采购需求 -》采购订单 -》发货
  * 仓库系统 -》拣货 -》包装 -》发货
  * SAP ECC -》发货单 -》发票
* 难点
  * 数据准备。准备多种不同类型订单，不同数量，按流程分别准备数据。存入 mysql。
  * 脚本。模拟 HTTP，（加密解密），模拟 SAP 流程，模拟 socket 数据，模拟 app
  * python 开发中间件，xml，gzip加密解密，修改参数
  * 准备几十台虚拟机，脚本自动安装，拷贝配置文件（新，老版本）
* 实现
  * Loadrunner编写 http 协议，SAP 协议，socket 协议脚本
  * QTP 编写 desktop 脚本
  * python 监控测试数据，实时日志
  * 分模块逐步测试，然后联合测试
* 问题
  * 高并发时，脚本报错
    * 测试帐号有限，产生冲突
    * 数据库中管理帐号，仍然错误
    * mysql 写存储过程，标识帐号使用中。
  * 第一次联合测试，响应极慢，终止测试
    * 测试数据问题。使用了少量的客户号，生成订单时，SAP数据库锁
    * 重新准备测试数据
  * 发现仓库系统慢 sql
    * 调优，建索引，重新测试

### 保险系统性能测试

* 背景

  * 中途接手，了解问题

  * 保险业务流程复杂，测试脚本编写困难（条款，审核，修改。。。）

* 实现

  * loadrunner

* 问题

  * 测试中遇到突然系统无响应，过一段时间恢复
  * 查日志
  * GC
  * 内存泄露

* 解决

  * 修复内存泄露
  * 调整内存分配

### SAML 接口测试

背景

* single single on 系统
* 测试公司内所有系统正确接入

难点

* 请求响应错误，没有明确信息。
* 逐个请求抓包，分析内容，调试

流程

* 打开目标系统 url
* 返回403 -》转入微软登录界面
* 输入帐号密码
*  saml 请求转入公司身份验证
* 验证通过，生成密钥，返回 saml 响应至微软
* 微软返回成功，header 中加入 token 登录至客户端
* 后续请求中header 中加入 token，后面所有请求都要包含 token

难点

* saml 解析，字段多，还有密钥，时间

## BPC

* 脚本 fiddler 抓包，转换 loadrunner
* 参数复杂xml，json
* python 抓 batch result



## 数据库调优

* 只读需要的列
* where 和 order by 要有 index
* 多字段 index，要按顺序
* 索引占空间，大量插入性能会下降
* where 不要写<>, not in
* 减少 join
* 大小表 join，先读出小表，再程序中处理，再读大表
* SQL trace 看 DB time

案例

* 将多次单条数据查询合并为范围查询
* 大表 join，字符串慢，整形快
* partition 按段分

## TCP

### 三次握手

client: 第一次握手(SYN=1, seq=x): 客户端进入 `SYN_SEND` 状态

server: 第二次握手(SYN=1, ACK=1, seq=y, ACKnum=x+1): 服务器端进入 `SYN_RCVD` 状态。

client: 第三次握手(ACK=1，ACKnum=y+1) 发送完毕后，客户端进入 `ESTABLISHED` 状态

### 四次挥手

client: 第一次挥手(FIN=1，seq=x) 客户端进入 `FIN_WAIT_1` 状态。

server: 第二次挥手(ACK=1，ACKnum=x+1) 发送完毕后，服务器端进入 `CLOSE_WAIT` 状态，客户端接收到这个确认包之后，进入 `FIN_WAIT_2` 状态，等待服务器端关闭连接。

server: 第三次挥手(FIN=1，seq=y) 发送完毕后，服务器端进入 `LAST_ACK` 状态

client: 第四次挥手(ACK=1，ACKnum=y+1) 服务器端接收到这个确认包之后，关闭连接，进入 `CLOSED` 状态

### TCP KeepAlive

TCP KeepAlive 的基本原理是，隔一段时间给连接对端发送一个探测包，如果收到对方回应的 ACK，则认为连接还是存活的，在超过一定重试次数之后还是没有收到对方的回应，则丢弃该 TCP 连接。

https://hit-alibaba.github.io/interview/

## 数据库 CPU 高

常见原因

系统执行应用提交查询（包括数据修改操作）时需要大量的逻辑读（逻辑 IO，执行查询所需访问的表的数据行数），所以系统需要消耗大量的 CPU 资源以维护从存储系统读取到内存中的数据一致性。

#### 应用负载（QPS）高

##### 现象描述

- **特征：**实例的 QPS（每秒执行的查询次数）高，查询比较简单、执行效率高、优化余地小。
- **表现：**没有出现慢查询（或者慢查询不是主要原因），且 QPS 和 CPU 使用率曲线变化吻合。
- **常见场景：**该状况常见于应用优化过的在线事务交易系统（例如订单系统）、高读取率的热门 Web 网站应用、第三方压力工具测试（例如 Sysbench）等。

##### 解决方案

对于由应用负载高导致的 CPU 使用率高的状况，使用 SQL 查询进行优化的余地不大，建议您从应用架构、实例规格等方面来解决，例如：

- 升级实例规格，增加 CPU 资源。

#### 查询执行成本（查询访问表数据行数 avg_lgc_io）高

##### 现象描述

- **特征：**实例的 QPS（每秒执行的查询次数）不高；查询执行效率低、执行时需要扫描大量表中数据、优化余地大。
- **表现：**存在慢查询，QPS 和 CPU 使用率曲线变化不吻合。
- **原因分析：**由于查询执行效率低，为获得预期的结果即需要访问大量的数据（平均逻辑 IO高），在 QPS 并不高的情况下（例如网站访问量不大），就会导致实例的 CPU 使用率高。

##### 解决方案

解决该状况的原则是：定位效率低的查询、优化查询的执行效率、降低查询执行的成本。

加 index

## 输入框

* 功能性
  * 常规字符 - 数字，字符串，特殊字符，转义字符
  * 非常规 - html 标签，css，javascript，url
  * 边界 - 边界值+1，-1，空字符，超长文本
* 兼容性
  * 手机品牌，分辨率，topN
  * 浏览器
  * 页面渲染，页面布局 - 渲染速度
* 稳定性
  * 压力下，正常返回结果
  * 多次查询，返回结果稳定
* 性能
  * QPS
  * 从点击到页面完全加载，平均耗时
  * 加载页面大小，资源（js，css）数量
* 安全
  * js 注入，sql 注入
* 接口
  * 查询接口正确性验证
  * 异常数据容错情况
  * 接口在非浏览器环境下处理情况
* 线上监控
  * 建立实时监控
  * 及时发现异常
* 自动化
  * Selenium UI 自动化
  * 回归验证
    * 截图，图像比对