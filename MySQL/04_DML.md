
## DML 语言基本介绍

数据操作语言：

1. 插入：`insert`
2. 修改：`update`
3. 删除：`delete`

## 插入语句

语法：

1. `insert into 表名(列名1,...)
   values(值1,...),(值1,...),...;`
2. `insert into 表名 set 列名=值,列名=值,...`

特点：

1. 插入的值的类型要与列 的类型一致或兼容
2. 插入的列的个数和值的个数必须一致
3. 不可以为 `null` 的列必须插入值，可以为 `null` 的值，可以将列名和值都省略或者直接用 `null` 填充
4. 列的顺序可以调换
5. 可以省略列名，默认所有列，而且列的顺序和表中列的顺序一致
6. 第一种支持一次插入多个数据，也支持子查询。第二种方式不支持

```sql
insert into beauty(id,name,phone)
values(1,'二狗','12345678'),(2,'三莽','987654321');

insert into beauty(id,name,phone)
select id,boyname,'3546123'
FROM boys WHERE id < 3;

insert into beauty
set id=3,name='四喜',phone='345125756';
```

## 修改语句

语法：

1. `update 表名 set 列=新值,列=新值,... where 筛选条件;`
2. `update 表1 别名 inner|left|right join 表2 别名 on 连接条件 set 列=值,... where 筛选条件;`

```sql
#修改单表的数据
UPDATE beauty SET phone='138998888888'
WHERE name LIKE '唐%';

UPDATE boys SET boyname='张飞',usercp=10
WHERE id=2;

#修改多表的数据
UPDATE boys bo
INNER JOIN beauty b ON bo.id=b.boyfriend_id
SET b.phone='128469'
WHERE bo.boyname='张无忌';

UPDATE boys bo
RIGHT JOIN beauty b ON bo.id=b.boyfriend_id
SET b.boyfriend_id=2
WHERE b.id IS NULL;
```

## 删除语句

语法：

1. `delete from 表名 where 筛选条件;`
2. `delete [表1的别名][,表2的别名] from 表1 别名 inner|left|right join 表2 别名 on 连接条件 where 筛选条件;`
3. `truncate table 表名;`

```sql
DELETE FROM beauty WHERE phone LIKE '%9';

DELETE b
FROM beauty b
INNER JOIN boys bo ON b.boyfriend_id=bo.id
WHERE bo.boyname='张无忌';

DELETE b,bo
FROM beauty b
INNER JOIN boys bo ON b.boyfriend_id=bo.id
WHERE bo.boyname='黄晓明';
```

特点：

1. `delete` 可以加 `where` 条件，`truncate` 不能加
2. `truncate` 是删除表中所有数据，效率比 `delete` 高一些
3. 假如要删除的表中有自增长列，如果使用 `delete` 删除后，再插入数据，自增长列从断点开始。而 `truncate` 删除后，再插入数据，自增长列的值从 1 开始
4. `truncate` 删除没有返回值，`delete` 删除后有返回值
5. `truncate` 删除不能回滚，`delete` 删除后可以回滚
