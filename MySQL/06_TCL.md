
## TCL 语言基本介绍

1. 事务控制语言（Transaction Control Language）简称 TCL
2. 事务：一个或一组 SQL 语句组成的一个执行单元，这个执行单元要么全部执行，要么全部不执行。
3. 存储引擎（表类型）：
   1. 概念：在 MySQL 中的数据使用不同的技术存储在文件（或内存）中
   2. 通过`show engines;` 来查看 MySQL 支持的存储引擎
   3. 在 MySQL 中使用最多的存储引擎有：**innodb**、**myisam**、**memory**等。其中  **innodb** 支持事务，也是默认引擎。而 **myisam**（5.1 版本之前默认引擎） 、**memory** 等不支持事务

## 事务

1. 概念：一个或一组 SQL 语句组成的一个执行单元，在这个单元中，每个 SQL 语句是相互依赖的。而整个单独单元作为一个不可分割的整体，如果单元中某条 SQL 语句一旦执行失败或产生错误，整个单元将会回滚，所有受到影响的数据将返回到事务开始之前的状态；如果单元中所有 SQL 语句均执行成功，则事务被顺利执行。
2. 事务的 ACID 属性：
   1. 原子性（Atomicity）：原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么不发生。
   2. 一致性（Consistency）：事务必须使数据库从一个一致性状态变换到另外一个一致性状态
   3. 隔离性（Isolation）：事务的隔离性是指一个事务的执行不能被其他事务干扰，即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能相互干扰。
   4. 持久性（Durability）：持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来的其他操作和数据库故障不应该对其有任何影响

### 事务的创建

#### 隐式事务

定义：事务没有明显的开启和结束的标记。比如`deletel`、`update`、`insert`

#### 显式事务

定义：事务具有明显的开启和结束的标记

前提：必须先设置自动提交功能为禁用`set autocommit=0;`

步骤：

1. 开启事务：`set autocmmit=0;`
2. 编写事务中的 SQL 语句，一般使用的语句有：`select`、`insert`、`update`、`delete`
3. `savepoint char`：设置回滚点
4. 结束事务
   1. `commit;`：提交事务
   2. `rollback [to savepoint_char]`：回滚事务到指定节点，默认全部回滚

Tips：`delete` 语句在事务中支持回滚，`truncate` 语句在事务中不支持回滚操作

```sql
#开启事务
SET autocommit=0;
START TRANSACTION;   #可选
#编写一组事务语句
UPDATE account SET balance = 500 WHERE username='Leon';
UPDATE account SET balance =1500 WHERE username='Bob';
#结束事务
#ROLLBACK;  #回滚，即撤销
commit;     #提交
```

### 数据库的隔离级别

定义：一个事务与其他事务隔离的程度，称为隔离级别。

特点：数据库规定了多种事务隔离级别，不同隔离级别对应不同的干扰程度。隔离级别越高，数据一致性越好，但并发性越弱。

#### 常见事务并发问题

对于同时运行的多个事务，当这些事务访问**数据库中相同的数据**时，如果没有采取必要的隔离机制，就会导致以下的并发问题：

1. 脏读：对于两个事务 T1、T2，T1 读取了已经被 T2 更新但还**没有被提交**的字段。之后如果 T2 回滚，T1 读取的内容就是临时且无效的
2. 不可重复读：对于两个事务 T1、T2，T1 读取了一个字段，然后 T2 **更新**了该字段。之后如果 T1 再次读取同一个字段，值就不一样了
3. 幻读：对于两个事务 T1、T2，T1 从一个表中读取了一个字段，然后 T2 再该表中**插入**了一些新的行。之后如果 T1 再次读取同一个表，就会多出几行

数据库事务的隔离性：数据库系统必须具有隔离并发运行各个事务的能力，使他们不会相互影响，避免各种并发问题

分类：

1. `READ UNCOMMITTED`（读取未提交）：允许事务读取未被其他事务提交的变更。脏读、不可重复和幻读的问题都会出现
2. `READ COMMITED`（读取已提交）：只允许事务读取已经被其他事务提交的变更。可以避免脏读，但不可重复读和幻读的问题仍然可能出现
3. `REPEATABLE READ`（可重复读）：确保事务可以多次从一个字段读取相同的值。在这个事务持续期间，禁止其他事务对这个字段进行更新，可以避免脏读和不可重复读，但幻读的问题仍然存在
4. `SERIALIZABLE`（串行化）：确保事务可以从一个表中读取相同的行。在这个事务持续期间，禁止其他事务对该表执行插入、更新和删除操作，所有并发问题都可以避免，但性能十分低下

> Tips：每种数据库支持的隔离级别不一样
>
> 1. Oracle 支持两种事务隔离级别：`READ COMMITED` 和 `SERIALIZABLE`。默认事务隔离级别为 `READ COMMITED`
> 2. MySQL 支持四种事务隔离级别。默认事务隔离级别为 `REPEATABLE READ`

#### 在 MySQL 中设置隔离级别

每启动一个 MySQL 程序，就会获得一个单独的数据库连接。每个数即可连接都有一个**全局变量** `@@tx_isolation`，表示当前的事务隔离级别

查看当前的事务隔离级别：`select @@tx_isolation`

设置当前 MySQL 连接的隔离级别：`set session transaction isolation level 隔离级别;`

设置数据库系统的全局隔离级别：`set global transaction isolation level 隔离级别;`

## 视图

MySQL 从 5.0.1 版本开始提供视图功能（前期版本不完善，从 5.1 版本正式使用）。是一种虚拟存在的表，行和列的数据来自定义视图的查询中使用的表，并且是在使用视图时**动态生成的**，**只保存看 SQL 逻辑，比保存查询结果**

应用场景：

1. 多个地方用到同样的查询结果
2. 该查询结果使用的 SQL 语句较复杂

好处：

1. SQL 语句的重用
2. 简化了复杂的 SQL 操作
3. 保护数据，提高安全性

### 创建视图

语法：`create view 视图名 as 查询语句;`

```sql
#创建视图
CREATE VIEW myv1
AS
SELECT last_name,department_name,job_title
FROM employees e
JOIN departments d ON e.department_id = d.department_id
JOIN jobs j ON j.job_id = e.job_id;
#使用视图
SELECT * FROM myv1 WHERE last_name LIKE '%a%';
```

### 修改视图

语法：

1. `create or replace view 视图名 as 查询语句;`
2. `alter view 视图名 as 查询语句;`

### 删除视图

语法：`drop view 视图名,视图名,...;`

### 查看视图

语法：

1. `DESC 视图名;`
2. `show create view 视图名;`

### 更新视图

视图的可更新性和视图中查询的定义有关系，以下类型的视图时不能更新的：

1. 包含以下关键字的 SQL 语句：
   1. 分组函数
   2. `distinct`
   3. `group by`
   4. `having`
   5. `union`
   6. `union all`
2. 常量视图
3. `select` 中包含子查询
4. `join`
5. `from` 一个不能更新的视图
6. `where` 子句的子查询引用了 `from` 子句中的表
