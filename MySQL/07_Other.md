

## 变量

1. 系统变量：
   1. 全局变量
   2. 会话变量
2. 自定义变量
   1. 用户变量
   2. 局部变量

### 系统变量

说明：变量由系统提供，不是用户定义。属于服务器层面

使用的语法：

1. 查看所有的系统变量：`show global|[session] variables;`
2. 查看满足条件的部分系统变量：`show global|[session] variables like '%char%'`；
3. 查看指定的某个系统变量的值：`select @@[global.|session.]系统变量名;`
4. 为某个系统变量赋值：
   1. `set global|[session] 系统变量名 = 值;`
   2. `set @@global.|[session.]系统变量名 = 值;`

#### 全局变量

作用域：服务每次启动将为所有的全局变量赋初始值，针对所有的会话（连接）有效，但不能跨重启

```sql
SHOW GLOBAL VARIABLES;

SHOW GLOBAL VARIABLES LIKE '%char%';

SHOW GLOBAL @@global.autocommit;

SET @@global.autocommit=0;
```

#### 会话变量

作用域：仅仅针对当前会话（连接）有效

```sql
SHOW SESSION VARIABLES;

SHOW VARIABLES LIKE '%char%';

SHOW @@tx_isolation;

SET SESSION tx_isolation='read-uncommitted';
```

### 自定义变量

说明：变量由用户自定义，不是由系统创建

步骤：声明、赋值、使用（查看、比较、运算）

#### 用户变量

作用域：只针对于当前会话（连接）有效，同于会话变量的作用域。使用位置不受限制可以在当前会话的 `begin end` 中，也可以在当前会话 `begin end` 之外

赋值操作赋：`=` 或 `:=`

1. 声明并初始化
   1. `set @用户变量名=值;`
   2. `set @用户变量名:=值;`
   3. `select @用户变量名:=值;`
2. 赋值（更新用户变量的值）
   1. 和初始化一样的三种方式
   2. `select 字段 into @变量名 from 表;` 要求查询出的结果只有一个值
3. 使用
   1. 查看：`select @用户变量名;`

#### 局部变量

作用域：仅仅在定义它的 `begin end` 中有效

1. 声明：`declare 变量名 类型 [default 值];`
2. 赋值：和用户变量赋值方式一样，但 `set` 方式不需要使用 `@`，`select` 方式需要加 `@`
3. 使用：和用户变量使用方式一样，但不需要加 `@`

```sql
#用户变量
SET @m=1;
SET @n=2;
SET @sum = @m + @n;
SELECT @sum;

#局部变量
DECLARE m INT DEFAULT 1;
DECLARE n INT DEFAULT 2;
DECLARE sum INT;
SET SUM=m+n;
SELECT SUM;
```

## 存储过程和函数

存储过程和函数类似于编程语言中的方法

好处：

1. 提高代码的重用性
2. 简化操作
3. 减少了编译次数并且减少了和数据库服务器的连接次数，提高效率

### 存储过程

含义：一组预先编译好的 SQL 语句的集合，可以理解成批处理语句

1. 创建语法：`create procedure 存储过程名(参数列表) begin 存储过程体(一组合法的 SQL 语句) end`

   Tips：

   1. 参数列表包含三部分：参数模式、参数名、参数类型。例如 `IN stuname VARCHAR(20)`

      > 参数模式：
      >
      > `IN`：该参数可以作为输入，即该参数需要调用方传入值
      >
      > `OUT`：该参数可以作为输出，即该参数可以作为返回值
      >
      > `INOUT`：该参数既可以作为输入又可以作为输出，即该参数既需要传入值，又可以返回值

   2. 如果存储过程体只有一句话，则 `begin end` 可以省略。存储过程体中的每句 SQL 语句结尾必须加分号。

   3. 在存储过程最开始使用 `DELIMITER char（结束标记）` 设置一个结束标记

   4. 参数列表可以为空，也可以为多个用逗号隔开

2. 调用语法：`call 存储过程名(实参列表)结束标记`

3. 删除存储过程：`DROP PROCEDURE 存储过程名;` 每次只能删除一个

4. 查看存储过程信息：`show create procedure 存储过程名;`

```sql
#空参列表的存储过程
DELIMITER $
CREATE PROCEDURE myp1()
BEGIN
   INSERT INTO admin(username,password)
   VALUES('johnl','0000'),('lily','0000'),('rose','0000'),('jack','0000'),('tom','0000');
END $

CALL myp1()$

#in 模式参数的存储过程
DELIMITER $
CREATE PROCEDURE myp2(IN username VARCHAR(20),IN password VARCHAR(20))
BEGIN
   DECLARE result INT DEFAULT 0;
   SELECT COUNT(*) INTO result
   FROM admin
   WHERE admin.username = username
   AND admin.password = password;
   SELECT IF(result>0,'成功','失败');
END $

CALL myp2('Leon','123456')$

#out 模式参数的存储过程
DELIMITER $
CREATE PROCEDURE myp3(IN beautyName VARCHAR(20),IN boyName VARCHAR(20))
BEGIN
   SELECT bo.boyName
   FROM boys bo
   INNER JOIN beauty b ON bo.id = b.boyfriend_id
   WHERE b.name=beautyName;
END $
SET @bName$
CALL myp3('小昭',@bName)$
SELECT @bName$

#inout 模式参数的存储过程
DELIMITER $
CREATE PROCEDURE myp4(INOUT a INT,INOUT b INT)
BEGIN
   SET a=a*2;
   SET b=b*2;
END $

SET @m=10$
SET @n=20$
CALL myp4(@m,@n)$
SELECT @n,@m$
```

### 函数

含义和好处和存储过程一样，但区别在于存储过程可以没有返回，也可以又多个返回，适合做批量插入和批量更新，但函数有且仅有一个返回，适合做处理数据后返回一个结果

1. 创建语法：`create function 函数名(参数列表) returns 返回类型 begin 函数体 end`

   Tips：

   1. 参数列表包含两部分：参数名、参数类型
   2. 函数体必须有 return 语句，return 语句一般放在函数体结尾处
   3. 函数体中只有一句话时，可以省略 `begin end`
   4. 使用 `delimiter` 语句设置结束标记

2. 调用语法：`select 函数名(参数列表)` 执行函数并显示返回值

3. 查看函数：`show create function 函数名;`

4. 删除函数：`drop function 函数名;`

```sql
#无参有返回
DELIMITER $
CREATE FUNCTION myf1() RETURNS INT
BEGIN
   DECLARE c INT DEFAULT 0;
   SELECT COUNT(*) INTO c
   FROM employees;
   RETURN c;
END $

SELECT myf1()$

#有参有返回
DELIMITER $
CREATE FUNCTION myf2(empName VARCHAR(20)) RETURNS DOUBLE
BEGIN
   SET @sal=0;
   SELECT salary INTO @sal
   FROM employees
   WHERE last_name = empName;

   RETURN @sal;
END $

SELECT myf2('Leon')$
```

## 流程控制结果

1. 顺序结构：程序从上往下依次执行
2. 分支结构：程序从两条或多条路径中选择一条去执行
3. 循环结构：程序在满足一定条件的基础上，重复执行一段代码

### 分支结构

1. IF 函数

   功能：实现简单的双分支

   语法：`IF(表达式1,表达式2,表达式3)`，如果表达式 1 成立，则返回表达式 2 的值，否则返回表达式 3 的值

2. case 结构

   1. 等值判断：

      ```sql
      CASE 变量|表达式|字段|函数
      WHEN 要判断的值1 THEN 返回的值1或语句1
      WHEN 要判断的值2 THEN 返回的值2或语句2
      ...
      ELSE 要返回的值n或语句n
      END [CASE];
      ```

   2. 区间判断

      ```sql
      CASE
      WHEN 要判断的条件1 THEN 返回的值1或语句1
      WHEN 要判断的条件2 THEN 返回的值2或语句2
      ...
      ELSE 要返回的值n或语句n
      END [CASE];
      ```

      特点：

      1. 当作为表达式嵌套在其他语句中使用，可以放在任何地方，`begin end` 中或`begin end` 外。
      2. 当作为独立语句使用时，只能放到 `begin end` 中，且 end 后必须跟 case，`then` 后必须时语句而且每条语句后必须加分号
      3. `else` 语句可以省略，且当所有条件都不满足时，则返回 NULL

      ```sql
      #case做独立语句使用
      DELIMITER $
      CREATE PROCEDURE myp1(IN score INT)
      BEGIN
         CASE
         WHEN score>=90 AND score<=100 THEN SELECT 'A';
         WHEN score>=80 THEN SELECT 'B';
         WHEN score>=60 THEN SELECT 'C';
         ELSE SELECT 'D';
         END CASE;
      END $
      CALL myp1(95)$
      ```

3. IF 结构

   功能：实现多重分支，且只能在 `begin end` 中使用

   ```sql
   #语法
   if 条件1 then 语句1;
   elseif 条件2 then 语句2;
   ...
   [else 语句n;]
   end if;

   #示例
   DELIMITER $
   CREATE FUNCTION myf1(score INT)
   BEGIN
      IF score>=90 AND score<=100 THEN SELECT 'A';
      ELSEIF score>=80 THEN SELECT 'B';
      ELSEIF score>=60 THEN SELECT 'C';
      ELSE SELECT 'D';
      END IF;
   END $

   CALL myf1(86)$
   ```

### 循环结构

分类：`while`、`loop`、`repeat`

循环控制：

1. `iterate`：类似 `continue` 继续。结束本次循环，继续下次循环
2. `leave`：类似 `break` 跳出，结束当前所在的循环

语法：

```sql
#while
[标签: ]while 循环条件 do
   循环体;
end while[ 标签];

#loop
[标签: ]loop
   循环体;
end loop;

#repeat
[标签: ]repeat
   循环体;
until 结束循环的条件
end repeat[ 标签];
```

特点：`while` 时先判断后执行，`repeat` 是先执行后判断，`loop` 是没有条件的死循环

示例：

```sql
#无循环控制
DELIMITER $
CREATE PROCEDURE myw1(IN insertCount INT)
BEGIN
   DECLARE i INT DEFAULT 1;
   WHILE i <= insertCount DO
      INSERT INTO admin(username,password) VALUES(CONCAT('ROSE',i),'666');
      SET i=i+1;
   END WHILE;
END $

CALL myw1(100)$

#有循环控制
DELIMITER $
CREATE PROCEDURE myw1(IN insertCount INT)
BEGIN
   DECLARE i INT DEFAULT 1;
   a:WHILE i <= insertCount DO
   INSERT INTO admin(username,password) VALUES(CONCAT('ROSE',i),'666');
   IF i>=20 THEN LEAVE a;
      END IF;
      SET i=i+1;
   END WHILE a;
END $

CALL myw1(100)$

#添加 iterate 语句
DELIMITER $
CREATE PROCEDURE myw1(IN insertCount INT)
BEGIN
   DECLARE i INT DEFAULT 0;
   a:WHILE i <= insertCount DO
      SET i=i+1;
      IF　MOD(i,2) THEN ITERATE a;
      END IF
      INSERT INTO admin(username,password) VALUES(CONCAT('ROSE',i),'666');
   END WHILE a;
END $

```
