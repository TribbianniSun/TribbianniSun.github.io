# 浅谈query_processing


[浅谈query_processing](https://blog.csdn.net/u013007900/article/details/78015124)
<!--more-->



我们知道，目前通用的数据库查询语言是SQL语言（Structured Query Language）。SQL语言也是一种编译型语言，需要SQL编译器编译后才能执行，但它与C、C++、Java等语言不同，SQL语言是一种非过程化语言，这意味着使用SQL进行操作的时候，你只需要指定你要达到什么目的，而无需指明要怎样达到目的。
既然用户只需要解决“做什么”的问题，那么，“怎么做”的问题正是本文要讨论的问题。



## 优化器（Optimizer）

优化器也称查询优化器（Query Optimizer），它的主要工作是优化数据访问，根据提交的SQL语句，综合各种已有的信息（主要是系统编目表）来产生最优的可执行的访问方案。

优化器在整个数据库系统中占据着至高无上的地位，它是数据库性能的决定因素，是所有数据库引擎中最重要的组件。

优化器的工作可以直观的理解为以下4个步骤：

- 接收并验证SQL语句的语法语义；
- 分析环境并优化满足SQL语句的方法；
- 创建计算机可读指令来执行优化的SQL；
- 执行指令或存储他们以便将来执行。

## 查询过程

![](https://img-blog.csdn.net/20170918050036343?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzAwNzkwMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

SQL Query -> Parse Query -> Check Semantics -> Rewrite Query -> Optimize Access Plan -> Generate Executable Code -> Execute Plan

## 语法分析（Parse Query）
SQL语句被提交给SQL编译器，编译器通过语法树（Parse Tree）分析该语句，检查其语法，如果存在语法错误，编译器就停止处理并返回错误信息；如果不存在语法问题，编译器会将SQL语句转换为可被优化器分析的逻辑查询语句（关系代数relational algebra语句），并据此创建该查询的查询图模。


## 语义检查（Check Semantics）
语法分析完成后，编译器会根据查询图模型进行语义检查（比如检查语句中的数据类型是否与数据库的表列的数据类型一致），语义检查完成后也会将相关信息添加到查询图模型，包括参考约束，表检查约束，触发器，和视图信息等。

## 查询重写（Rewrite Query）
如果SQL语句的语法语义都没有问题，就可以正式进行查询操作了。这是优化器进行查询优化的开始阶段，其目的是将提交的SQL语句优化成效率更高的形式。
这种优化可以是基于查询成本的考虑，也可以是基于查询规则的考虑，是基于关系代数语句进行的调整。举一个直观的例子：

```
Select EMPLOYEE.Name, WELFARE.Bonus From EMPLOYEE, WELFARE Where EMPLOYEE.Seniority > 5 And  EMPLOYEE.Seniority = WELFARE.Seniority ;

Select EMPLOYEE.Name, WELFARE.Bonus From EMPLOYEE, WELFARE Where EMPLOYEE.Seniority > 5 And  WELFARE.Seniority > 5 And  EMPLOYEE.Seniority = WELFARE.Seniority ;
```

很显然，两条语句的功能相同，第二条后面的“WELFARE.Seniority > 5”条件还有点多余，那么，那条语句的执行效率更高？

答案是第二条！因为第一条将EMPLOYEE中Seniority>5的行与WELFARE中的所有行作外连接再来找Seniority相等的行，而第二条则是将EMPLOYEE中Seniority>5的行和WELFARE中Seniority>5的行作外连接再来找Seniority相等的行。显然，第二条语句只有更少的行参与外连接，效率自然更高。

可是，我们通常写出的查询语句都是第一条的形式，而查询重写却可以将之优化，优化器的查询重写器能自动帮我们完成查询语句的优化，找到更高效的查询形式。

当然了，查询重写并不是直接对SQL语句作上述例子那样的优化，它操作的是由语法分析转换过的关系代数语句，且需要根据重写图模型提供的信息作出形式优化。

## 优化访问计划（Optimizer Access Plan）
根据查询图模型提供的信息，优化器会生成许多能够满足查询请求的访问计划（执行方案方案），然后优化器综合系统编目表中关于表，索引，列和函数等等的统计信息，估计每种访问计划的执行成本，并选择具有最小成本的方案作为最终的访问计划（Acess Plan）。

## 生成可执行代码（Generate Executable Code）
根据最终选定的访问计划生成执行代码，类似C语言编译后生成可被机器识别的机器码一样。

## 执行访问计划（Execute Plan）
执行可执行代码，获取查询结果集。




