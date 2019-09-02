## UI automation test framework

### 基于业务流程设计测试用例

业务需求 -- 功能需求 -- 测试需求 -- 测试用例设计

* 基于Page object

Page.component.opreation(data)

* 以业务流程来描述测试用例

login -- search -- checkout -- logout

引入business flow，可跨多个page

flow可以output数据，传给下一个flow

flow的开始页面可以是上一个flow的结束页面

判断当前页面，来决定流程分支

```
doIfPageIs(PageA.class, () -> {
	start(new PageA()).
				.action(PageA::doSth)
				.action(PageA::gotoPageB)
})

```



### 测试数据

测试用例和测试数据分离

test data provider 读取json或者csv

测试数据准备

	* 调用api
	* db acccess
	* 基于Java的工具开发



* 把固定的测试数据在准备测试环境时就准备好，（商品分类）

* 动态数据，一次性数据，调用数据工具，产生数据，立即消耗。

### 测试数据准备

```
DataBuilder.build();
Databuilder.with(A).build()
Databuilder.with(B).with(C).
			.withBuildStrategy(BuildStrategy.CREATE_ONLY)
			.build();
```

不同数据创建的元数据（recipe），根据不同厂商，创建不同用户



策略：

* 创建
* 搜索
* 搜索优先，不存在则创建

### 测试数据管理UI

* Dashboard
  * 各种数据的总数量
* 按不同数据类型分类
  * 搜索，修改，添加



## API Automation Test Framework

- API层测试变得重要
- api设计文档 -- api测试用例设计
- 业务测试数据存入数据库，自动化生成部分典型异常数据
- 并发测试，多线程同时执行
- 结果验证，返回值比对，过滤变化值，有不同则报warning
- 微服务
  - api数量变多
  - 根据调用关系，覆盖有关联的测试用例



## 测试报告

* 测试失败，可能是环境问题，数据问题，等

生成 Full Trace report， 包含执行日志，数据，截图，方便开发直接定位问题

* 按需求生成story board，直观测试过程