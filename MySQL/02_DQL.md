# 数据库查询语言

## DQL 语言基本介绍

1. 数据库查询语言(Data Query Language)简称DQL，关键字`SELECT`

2. 基本语法``SELECT 查询列表 FROM 表名``

3. 特点：

   > 1. 查询列表可以是：表中的字段、常量值、函数、表达式
   > 2. 查询的结果是一个虚拟的表格(临时性的)

## 基础查询

1. 查询表中指定的字段

   > 语法：``SELECT 字段,字段,字段 FROM 表名``

2. 查询所有字段

   > 语法：``SELECT * FROM 表名``
   > Tips：指定查询按照指定的顺序排序，使用星号按照默认方式排序

3. 查询常量值和函数

   > 语法：``SELECT 常量值(函数)``
   > Tips：常量值包括整型，字符型(加单(双)引号)

4. 别名

   优点：便于理解，有重名的情况下便于区分，拼接字段是方便命名
   > 语法：
   >
   > > 1. SELECT 查询列表 AS 别名,查询列表 AS 别名 【FROM 表名】
   > > 2. SELECT 查询列表 别名,查询列表 别名 【FROM 表名】

   Tips：当查询语句中出现特殊符号是需要使用单(双)引号或着重号将该语句包含起来
   >例：`SELECT salary AS 'out put' FROM employees`

5. 去重

   > 语法：`SELECT DISTINCT 字段 FROM 表名;`

6. 拼接字段

   > 语法：`SELECT CONCAT(str,str,......)【AS 别名 FROM 表名】;`
   > Tips：str可以为任意查询列表，如果拼接的字段中有为NULL的，则结果为NULL，可使用IFNULL函数

7. IFNULL函数

   > 语法：IFNULL(可能为NULL的查询列表，返回值)
   > 作用：该函数只能用于判断该查询列表的值是否为NULL，如果为NULL则返回指定的返回值，否则返回原值
   > Tips：指定的返回值只能是数值型或字母

8. 加号的作用

   SQL语句中加号只能用作**运算符**

   | 示例              | 说明                                     |
   | ----------------- | ---------------------------------------- |
   | SELECT 100+90;    | 两个操作数都为数值型则做加法运算         |
   | SELECT '123'+123  | 若一方为字符则进行转换，成功则继续运算。 |
   | SELECT 'leon'+123 | 若转换失败，则字符的值为0，继续运算      |
   | SELECT NULL+123   | 若其中一方为NULL,则运算结果为NULL        |

## 条件查询

语法：`SELECT 查询列表 FROM 表名 WHERE 筛选条件`

Tips：该语句执行顺序为，先查看表名，然后判断筛选条件，再根据查询列表查询，最后显示查询结果

根据筛选方式可以分为三类：

1. 按照条件表达式筛选

   > 条件运算符包括：`>、<、=、<>即!=、>=、<=`
   > 例如：

   ```sql
   SELECT * FROM employees WHERE salary<12000 ;
   SELECT * FROM employees WHERE  salary>10000;
   ```

2. 按照逻辑表达式筛选

   > 逻辑运算符包括：`and、or、not即 &&、||、！`

   ```sql
   SELECT * FROM employees WHERE salary<12000 AND salary>10000;
   SELECT * FROM employees WHERE salary<12000 && salary>10000;
   ```

3. 按照模糊运算符筛选

   模糊运算符包括：`Like、Between and、in、Is null`

   > **Like**
   >  一般与通配符搭配使用，通配符有：`%`、`_`
   > Tips：
   > 百分号表示任意多个字符，下划线表示单个字符
   > 筛选条件为字符型需要加单(双)引号
   > 如果筛选条件中包含百分号和下划线，则使用`\`来进行转义，也可以使用ESCAPE指定转义符，如果使用字母作为转义符，则前后大小写要一致

   ```sql
   SELECT last_name FROM employees WHERE last_name LIKE '_e%n';
   SELECT last_name FROM employees WHERE last_name LIKE '_\_n';
   SELECT last_name FROM employees WHERE last_name LIKE '_A_n%' ESCAPE 'A';
   ```

   > **Between and**
   >
   > 1. 包含临界值，提高语句简洁度
   > 2. 两个临界值不能调换顺序
   > 3. 两个临界值的类型需要一致或能隐式转换

   ```sql
   SELECT last_name FROM employees WHERE salary<12000 && salary>10000;
   SELECT last_name FROM employees WHERE salary BETWEEN 10000 AND 12000;
   ```

   > **In**
   > 含义：判断某字段是否属于In列表中的某一项

   ```sql
   SELECT password FROM user WHERE host = '127.0.0.1' AND host = 'localhost';
   SELECT password FROM user WHERE host IN ('127.0.0.1','localhost');
   ```

   > **Is Null**
   > 当查询的值为NULL时，因为`=`和`<>`无法用于判断NULL，所以使用`Is Null`和`Is Not Null`
   > 假设commission_pct字段的值中存在NULL

   ```sql
   SELECT last_name,commission_pct FROM employees WHERE commission_pct IS NULL;
   SELECT last_name,commission_pct FROM employees WHERE commission_pct IS NOT NULL;
   ```

   > Tips：也可使用`<=>`(安全等于)来判断NULL值,当然也可以判断普通值

## 排序查询

语法：`select 查询列表 from 表 where 筛选条件 order by 排序列表 [ASC | DESC]`

Tips：

1. 降序使用 `DESC`，升序使用 `ASC` (可以省略)。默认是升序，从低到高
2. `order by` 子句中可以支持单个字段、多个字段、表达式、函数、别名
3. `order by` 子句一般放在查询语句的最后面，`limit`  子句除外

示例：

```sql
#单字段排序
SELECT * FROM employees ORDER BY salary DESC;
#多字段排序
SELECT * FROM employees ORDER BY salary ASC, employee_id DESC;
#表达式排序
SELECT *, salary*12*(1+IFNULL(commission_pct,0)) 年薪 FROM employees ORDER BY salary*12*(1+IFNULL(commission_pct,0)) DESC;
#函数排序
SELECT LENGTH(last_name) 姓名长度, last_name, salary FROM employees ORDER BY LENGTH(last_name);
#别名排序
SELECT *, salary*12*(1+IFNULL(commission_pct,0)) 年薪 FROM employees ORDER BY 年薪 DESC;
```

## 分组查询

```sql
/*
语法：
SELECT 分组函数, 需要分组的列（要求出现在 groud by 的后面）
FROM 表
[where 筛选条件]
group by 需要分组的列
[HAVING 筛选条件]
[order by 子句]
*/
#查询每个工种的最高工资
SELECT MAX(salsry), job_id
FROM employees
GROUP BY job_id;
#查询每个位置上的部门个数
SELECT COUNT(*), location_id
FROM departments
GROUP BY location_id;

#查询每个管理编号大于 102 的管理手下最低工资大于 5000 的员工的最低工资
SELECT MIN(salary), manager_id
FROM employees
WHERE manager_id > 102
GROUP BY manager_id
HAVING MIN(salary) > 5000;

#按照员工姓名的长度分组，查询每一组的员工个数，筛选员工个数大于 5 的有哪些
SELECT COUNT(*), LENGTH(last_name) len_name
FROM employees
GROUP BY len_name
HAVING COUNT(*)>5;

#查询每个部门，每个工种的员工的平均工资，并排序
SELECT AVG(salary),department_id,job_id
FROM employees
GROUP BY job_id,department_id
ORDER BY AVG(salary) DESC;
```

特点：分组查询中的筛选条件分为两类

1. 分组前筛选：数据源是原始表，位置在 `group by` 子句前面，关键字用 `where`
2. 分组后筛选：数据源是分组后的结果集，位置在 `group by` 子句后面，关键字用 `having`
3. `group by` 后支持多个字段作为分组条件，也支持表达式和函数作为分组条件

Tips：

1. 查询列表必须，要求是在分组函数和 `group by` 后出现的字段
2. MySQL 中支持在 `group by` 和 `having` 子句后使用别名，其他不一定支持（不通用）
3. 分组函数做条件一定是放在 `having` 子句中
4. 能用分组前筛选优先使用分组前的筛选（效率问题）
5. 排序必须放在语句最后

## 连接查询

含义：又称多表查询，当查询的字段来自多个表时就需要使用连接查询

分类：

1. 按年代分类
   1. SQL92 标准：仅支持内连接
   2. SQL99 标准（推荐）：支持内连接、交叉连接、外连接（左外和右外）
2. 按功能分类
   1. 内连接
      1. 等值连接
      2. 非等值连接
      3. 自连接
   2. 外连接
      1. 左外连接
      2. 右外连接
      3. 全外连接
   3. 交叉连接

> 笛卡尔乘积现象：表 1 有 m 行，表 2 有 n 行，查询结果为 `m*n` 行
>
> 发生原因：当查询多个表时，没有添加有效的连接条件，导致多个表所有行实现完全连接
>
> 解决方法：添加有效的连接条件

### SQL92 标准

1. 等值连接

   特点：

   1. 多表等值连接的结果为多表的交集部分
   2. n 表连接，至少需要 n-1 个连接条件
   3. 多表的顺序没有要求
   4. 一般需要为表起别名，如果使用了别名，则查询的字段就不能使用原来的表名去限定
   5. 可以搭配前面介绍的所有子句使用，如：排序、分组、筛选。筛选条件用 `and` 进行连接

   ```sql
   SELECT COUNT(*), city
   FROM departments AS d, location_id l
   WHERE d.location_id=l.location_id
   GROUP BY city;

   SELECT last_name,department_name,city,d.department_id
   FROM employees e,departments d,locations l
   WHERE e.department_id=d.department_id
   AND d.location_id=l.location_id
   ORDER BY department_name DESC
   ```

2. 非等值连接

   ```sql
   SELECT salary,grade_level
   FROM employees e,job_grades g
   WHERE salary BETWEEN g.lowest_sal AND g.highest_sal
   AND g.grade_level='A';
   ```

3. 自连接

   ```sql
   SELECT e.employee_id,e.last_name,m.employee_id,m.last_name
   FROM employees e,employees m
   WHERE e.employee_id=m.employee_id;
   ```

### SQL99 标准

特点：

1. 可以添加排序、分组、筛选
2. `inner` 和 `outer` 可以省略
3. 筛选条件放在 `where` 后面，连接条件放在 `on` 后面，提高分离性，便于阅读

语法：

```sql
select 查询列表
from 表1 别名
[连接类型] join 表2 别名
on 连接条件
[where 筛选条件]
[group by 分组]
[having 筛选条件]
[order by 排序列表]
```

1. 内连接

   连接类型为 `inner`

   ```sql
   #等值连接
   SELECT last_name,department_name
   FROM departments d
   INNER JOIN employees e
   ON e.department_id=d.department_id
   WHERE e.last_name LIKE '%e%';

   SELECT last_name,department_name,job_title
   FROM employees e
   INNER JOIN departments d ON e.department_id=d.department_id
   INNER JOIN jobs j ON e.job_id=j.job_id
   ORDER BY department_name DESC;

   #非等值连接
   SELECT COUNT(*),grade_level
   FROM employees e
   INNER JOIN job_grades g
   ON e.salary BETWEEN g.lowest_sal AND g.highest_sal;
   GROUP BY grade_level
   HAVING COUNT(*)>20
   ORDER BY grade_level DESC;

   #自连接
   SELECT e.last_name,m.last_name
   FROM employees e
   JOIN employees m
   ON e.manager_id=m.employee_id
   WHERE e.last_name LIKE '%k%';
   ```

2. 外连接

   应用场景：一个表中有，另一个表中没有的记录

   特点：

   1. 外连接的查询结果为主表中的所有记录

      > 如果从表中有和主表中匹配的，则显示匹配的值
      >
      > 如果从表中没有和主表中匹配的，则显示 NULL
      >
      > 外连接查询结果等于内连接结果和主表中有而从表中没有的记录
      >
      > 全外连接查询结果等于内连接结果和表 1 中没有但表 2 有的，和表 2 中有但表 1 中没有的

   2. 左外连接：`left outer join` 左边的是主表。右外连接：`right outer join` 右边的是主表

   3. 左外和右外交换两个表的顺序，可以实现同样的效果

   4. `MySQL` 不支持全外连接

   类型：

   1. 左外：连接类型为 `left [outer]`

      ```sql
      SELECT d.*,e.employee_id
      FROM departments d
      LEFT OUTER JOIN employees e
      ON d.department_id=e.department_id
      WHERE e.employee_id IS NULL;
      ```

   2. 右外：连接类型为 `right [outer]`

      ```sql
      SELECT d.*,e.employee_id
      FROM employees e
      RIGHT JOIN departments d
      ON d.department_id=e.department_id
      WHERE e.employee_id IS NULL;
      ```

   3. 全外：连接类型为 `full [outer]`

      ```sql
      SELECT b.*,bo.*
      FROM beauty b
      FULL OUTER JOIN boys bo
      ON b.boyfriend_id=bo_id
      ```

3. 交叉连接

   连接类型为 `cross`

   使用九九标准的语法实现的笛卡尔乘积

   ```sql
   SELECT b.*,bo.*
   FROM beauty b
   CROSS JOIN boys bo;
   ```

## 子查询

含义：出现在其他语句中的 `select` 语句，称为子查询或内查询。内部嵌套其他 `select` 语句的查询，称为外查询或主查询

分类：

1. 按查询出现的位置：
   1. `select` 后面：只支持标量子查询
   2. `from` 后面：支持表子查询
   3. `where` 或 `having` 后面：支持标量子查询（单行）和列子查询（多行），也支持行子查询（使用较少）
   4. `exists` 后面（相关子查询）：支持表子查询
2. 按结果集的行列数不同进行分类：
   1. 标量子查询（结果集只有一行一列）
   2. 列子查询（结果集只有一列多行）
   3. 行子查询（结果集有一行多列
   4. 表子查询（结果集一般为多行多列）

### where 或 having 后面

特点：

1. 子查询放在括号内
2. 子查询一般放在条件右侧
3. 子查询的执行优先于主查询的执行
4. 标量子查询，一般搭配单行操作符使用如：`> < >= <= = <>`
5. 列子查询一般搭配多行操作符使用如：`IN/NOT IN、ANY/SOME、ALL`

类型：

1. 标量子查询（单行子查询）

   ```sql
   SELECT last_name,job_id,salary
   FROM employees
   WHERE job_id=(
      SELECT job_id
       FROM employees
       WHERE employee_id=141
   ) AND salary>(
      SELECT salary
       FROM employees
       WHERE employee_id=143
   );


   SELECT MIN(salary),department_id
   FROM employees
   GROUP BY department_id
   HAVING MIN(salary)>(
      SELECT MIN(salary)
       FROM employees
       WHERE department_id=50
   );
   ```

2. 列子查询（多行子查询）

   ```sql
   SELECT last_name
   FROM employees
   WHERE department_id IN(
      SELECT DISTINCT department_id
       FROM departments
       WHERE location_id IN (1400,1700)
   );

   SELECT last_naem,employee_id,job_id,salary
   FROM employees
   WHERE salary < ALL(
      SELECT salary
       FROM employees
       WHERE job_id = 'IT_PROG'
   ) AND job_id <> 'IT_PROG';
   ```

   | 多行操作符  |                    含义                    |
   | :---------: | :----------------------------------------: |
   | IN / NOT IN |            等于列表中的任意一个            |
   | ANY \| SOME | 和子查询返回的结果集中的任意一个值进行比较 |
   |     ALL     |        和子查询返回的所有值进行比较        |

3. 行子查询（多行多列）

   ```sql
   SELECT *
   FROM employees
   WHERE (employee_id,salary) = (
      SELECT MIN(employee_id),MAX(salary)
       FROM employees
   );
   ```

   要求：筛选条件的操作符必须一致，如都是等于或都是大于

### select 后面

Tips：仅支持标量子查询

```sql
SELECT d.* (
   SELECT COUNT(*)
    FROM employees e
    WHERE e.department_id=d.department_id
) 个数
FROM departments d;
```

### from 后面

将子查询结果充当一张表，要求必须起别名

```sql
SELECT ag_dep.*,g.level
FROM (
   SELECT AVG(salary) ag,department_id
    FROM employees
    GROUP BY department_id
) ag_dep
INNER JOIN job_grades g
ON ag_dep.ag BETWEEN g.lowest_sal AND g.highest_sal;
```

### exists 后面（相关子查询）

语法：`exists(完整的查询语句)`

结果：1 和 0，返回结果有值为 1，没有值为 0

```sql
SELECT department_name
FROM departments d
WHERE EXISTS(
   SELECT *
    FROM employees e
    WHERE d.department_id=e.department_id
);
```

## 分页查询

语法：`limit offset,size` `offset` ：要显示条目的起始索引（起始索引从 0 开始）。`size` ：要显示的条目个数。

特点：

1. `limit` 语句放在查询语句的最后

2. 公式：要显示的页数为 page，每页显示的条目数为 size。

   则语句为 `limit (page-1)*size,size`

```sql
SELECT * FROM employees LIMIT 5;
SELECT * FROM employees LIMIT 10,15;
```

## 联合查询

关键字：`union [all]`

作用：将多条查询语句的结果合并成一个结果

语法：

```sql
查询语句1
union [all]
查询语句2
union [all]
......
```

应用场景：要查询的结果来自多个表，且多个表没有直接的连接关系，但查询的信息一致时

特点：

1. 要求多条查询语句的查询列数是一致的
2. 要求多条查询语句的查询的每一列的类型和顺序最好一致
3. `union` 关键字默认是去重的，使用 `union all` 可以查询重复项
