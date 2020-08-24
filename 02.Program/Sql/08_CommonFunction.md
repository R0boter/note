# 基础函数

## 函数基本

概念：类似编程语言中的方法、函数，是将一组逻辑语句封装在方法体中，对外暴露方法名

好处：

1. 隐藏了实现细节
2. 提高代码的重用性

分类：

1. 单行函数
2. 分组函数：做统计使用，又称为统计函数、聚合函数、组函数

## 单行函数

1. 字符函数

   ```sql
   #1. length(str) 获取参数值的字节个数，utf8下汉字为3字节，GBK下为2字节
   SELECT LENGTH('Leon');
   #2. concat(str,str,...) 拼接字符串
   SELECT CONCAT(last_name,'_',first_name) 姓名 FROM employees;
   #3. upper(str)、lower(str) 将字符串转换为大写、小写
   SELECT CONCAT(UPPER(last_name),LOWER(first_name)) 姓名 FROM employees;
   #4. substr(str,index[,step]) 截取字符串中从指定下标处指定步长的字符，如没有指定步长，则默认截取到末尾
   SELECT CONCAT(UPPER(SUBSTR(last_name,1,1)),'_',LOWER(SUBSTR(last_name,2))) 姓 FROM employees;
   #5. instr(str,substr) 返回子字符串在指定字符串中第一次出现的索引，找不到返回0
   SELECT INSTR('My name is Leon','Leon') AS out_put;
   #6. trim([str FROM ]str) 去除字符串前后的指定字符，默认是去除前后空格
   SELECT TREIM('     Leon     ') AS out_put;
   SELECT TREIM('a' FROM 'aaaaaaaaaaaaLeonaaaaaaaa');
   #7. lpad(str,len,padstr) 用指定的填充字符将目标字符串左填充到指定长度
   SELECT LPAD('Leon',10,'*') AS out_put;
   #8. rpad(str,len,padstr) 用指定的填充字符将目标字符串右填充到指定长度
   SELECT RPAD('Leon',10,'*') AS out_put;
   #9. replace(str,str,str) 替换字符串中所有的指定的字符
   SELECT REPLACE('My name is Leon','Leon','Tommy') AS out_put;

   ```

2. 数学函数

   1. `round(flot[, num])`  四舍五入，可指定保存小数点后几位
   2. `ceil(flot)` 向上取整，返回 >= 该参数的最小整数
   3. `floor(flot)` 向下取整，返回 <= 该参数的最大整数
   4. `truncate(flot, num)` 截取参数的小数点后 num 位
   5. `mod(num, nnum)` 取余，前面是被除数，后面是除数
   6. `rand()` 获取随机数，返回 0-1 之间的小数

3. 日期函数

   1. `now()` 返回当前系统日期和时间

   2. `curdate()` 返回当前系统的日期

   3. `curtime()` 返回当前系统的时间

   4. 获取指定的部分，年、月、日、小时、分钟、秒

      ```sql
      year();
      month();
      monthname();
      day();
      hour();
      minute();
      second();
      ```

   5. `str_to_data(str, format)` 将日期格式的字符转换为指定的格式

       ```sql
      SELECT STR_TO_DATA('4-3 1992','%c-%d %Y') AS out_put;
      ```

   6. `data_format(data,format)` 将日期转换成字符

       ```sql
       SELECT DATE_FORMAT(NOW(),'%Y年%M月%d日') AS out_put;
       ```

   7. `datadiff(data,data)` 返回两个时间的差，用第一个日期减第二个日期

       ```sql
       SELECT DATADIFF(now(), '1993-1-1');
       ```

4. 其他函数

   1. `version()` 查看当前数据库版本
   2. `database()` 查看当前使用的数据库名
   3. `user()` 查看当前连接数据库的用户
   4. `password(str)` 返回字符的密码形式（加密）
   5. `md5(str)` 返回 md5 加密后的密文

5. 流程控制函数

   1. `if(expr1,expr2,expr3)` 根据条件表达式 1 判断，成立（true）返回 expr2 的值，不成立（false）返回 expr3 的值

      ```sql
      SELECT last_name, commission_pct,IF(commission_pct IS NULL, '没奖金', '有奖金') 备注 FROM employees;
      ```

   2. `case`

      1. 等值判断

         ```sql
         case 变量|表达式|函数
         when 常量1 then 值1
         when 常量2 then 值2
         ...
         else 值n
         end
         ```

      2. 区间判断

         ```sql
         case
         when 条件1 then 值1
         when 条件2 then 值2
         ...
         else 值n
         end
         ```

| 格式符 |           功能            |
| :----: | :-----------------------: |
|   %Y   |        四位的年份         |
|   %y   |        两位的年份         |
|   %m   | 月份（01，02，03…11，12） |
|   %c   |  月份（1，2，3…11，12）   |
|   %d   |       日（01，02…）       |
|   %H   |     小时（24小时制）      |
|   %h   |     小时（12小时制）      |
|   %i   |     分钟（01，02…59）     |
|   %s   |    秒（01，02，03…59）    |

## 分组函数

```sql
sum() #求和
avg() #平均值
max() #最大值
min() #最小值
count() #统计个数
```

 特点：

1. sum 和 avg 一般用于数值型数据，max、min 和 count 可以处理任何数据类型

2. 以上分组函数都忽略 NULL 值

3. 配合 DISTINCT 搭配可以去除数据中的重复数据

   ```sql
   SELECT SUM(DISTINCT salary) FROM employees;
   ```

4. `count()` 的特殊使用

   ```sql
   #统计行数可以使用以下三种方式
   SELECT count(salary) FROM employees;
   SELECT count(*) FROM employees;
   SELECT count(1) FROM employees;
   ```

   TIPS：

   1. MySQL 5.5 版本之前使用的存储引擎是 MYISAM，之后使用的存储引擎是 INNODB
   2. MYISAM 引擎下 `count(*)` 效率最高，因为该引擎有一个内部寄存器直接返回这个值
   3. INNODB 引擎下 `count(*)` 和 `count(1)` 效率一样，都高于 `count(字段)`

5. 和分组函数一同查询的字段有限制，和分组函数一同查询的要求是 `group by` 后的值
