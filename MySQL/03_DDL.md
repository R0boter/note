# 数据库定义语言

## DDL  语言基本介绍

数据定义语言

1. 库的管理：创建、修改、删除
2. 表的管理：创建、修改、删除

关键字：

1. 创建：`create`
2. 修改：`alter`
3. 删除：`drop`

## 库的管理

1. 库的创建

   语法：`create database [if not exists] 库名;`

   特点：

   1. 库名具有唯一性，如果库名已存在则报错，使用中括号中的可以判断库是否存在，不存在则创建，存在则不创建
   2. 创建时可以指定字符集 `character set utf8`，如果不指定则使用默认字符集（由系统默认字符集决定）

2. 库的修改

   1. 库名的修改：`rename database 旧库名 to 新库名;` **此语句只能用于 5.1 版本以前，切会造成数据错误**。
   2. 更改库的字符集：`alter database 库名 character set utf8`

3. 库的删除

   语法：`drop database [if exists] 库名;`

## 表的管理

1. 表的创建

   语法：`create table [if not exists] 表名(列名 列的类型[(长度) 约束],列名 列的类型[(长度) 约束],...)`

   ```sql
   CREATE TABLE book(
      id INT,
       bname VARCHAR(20),
       price DOUBLE,
       authorId INT,
       publishDate DATETIME
   );
   ```

2. 表的修改

   语法：`alter table 表名 add|drop|modify|change column 列名 [列类型 约束];`

   ```sql
   #修改列名
   ALTER TABLE book CHANGE COLUMN publishDate pubDate DATETIME;

   #修改列的类型或约束
   ALTER TABLE book MODIFY COLUMN pubdate TIMESTAMP;

   #添加新列
   ALTER TABLE author ADD COLUMN annual DOUBLE [first|after pubdate];

   #删除列
   ALTER TABLE author DROP COLUMN annual;

   #修改表名
   ALTER TABLE author RENAME TO book_author;
   ```

3. 表的删除

   语法：`DROP TABLE [if exists] 表名;`

4. 表的复制

   1. 只复制表的结构：`create table 新表名 like 旧表名;`

   2. 复制表的结构和数据：`create table 新表名 select 列名,列名,... from 旧表名 [where 筛选条件];`

      ```sql
      #复制结构
      CREATE TABLE copy LIKE author;

      #复制表的结构和数据
      CREATE TABLE copy1
      SELECT * FROM author;

      #复制部分数据
      CREATE TABLE copy2
      SELECT id,au_name
      FROM author
      WHERE nation='中国';

      #只复制部分结构
      CREATE TABLE copy3
      SELECT id,au_name
      FROM author
      WHERE 1=2;
      ```

## 常见数据类型

1. 数值型：
   1. 整形
   2. 小数：
      1. 定点数
      2. 浮点数
2. 字符型：
   1. 较短的文本：char、varchar
   2. 较长的文本：text、blob（较长的二进制数据）
3. 日期型

### 数值型

#### 整型

分类：

1. tinyint：占 1 字节，有符号：-2^7 ~ 2^7-1 无符号：0 ~ 2^8-1
2. Smallint：占 2 字节，有符号：-2^15 ~ 2^15-1 无符号：0 ~ 2^16-1
3. Mediumint：占 3 字节，有符号：-2^23 ~ 2^23-1 无符号：0 ~ 2^24-1
4. Int、Integer：占 4 字节，有符号：-2^31 ~ 2^31-1 无符号：0 ~ 2^32-1
5. Bigint：占 8 字节，有符号：-2^63 ~ 2^63-1 无符号：0 ~ 2^64-1

特点：

1. 默认为有符号，要设置无符号需添加 `unsigned` 关键字
2. 当插入数值超出类型的数值范围，则插入的是临界值，且会报 `out of range` 异常
3. 当不设置长度，会有默认长度。长度代表显示的最小宽度，如果不够会在左侧使用 0 填充，需在定义类型时搭配 `zerofill` 使用，使用后则类型为无符号型

#### 浮点数

类型

1. 浮点型：

   1. `float(M,D)`：占 4 字节，+-1.75494351E-38 ~ +-3.402823566E+38
   2. `double(M,D)`：占 8 字节，+-2.2250738585072014E-308 ~ +-1.7976931348623157E+308
2. 定点型：
   1. `dec(M,D)`：占 M+2 字节，最大取值范围和 double 相同，给定 decimal 的有效取值范围由 M 和 D 决定
   2. `decimal(M,D)`：占 M+2 字节，最大取值范围和 double 相同，给定 decimal 的有效取值范围由 M 和 D 决定

特点：

1. M：代表整数位和小数位的总长度。D：代表小数位长度。如果超出范围则插入临界值
2. M 和 D 可以省略，如果是 decimal，则 M 默认为 10，D 默认为 0 。如果是浮点型，则会根据插入的数值的精度来决定精度
3. 定点型的精确度较高，如果要求插入数值的精度较高，如货币运算，则优先考虑

### 字符型

#### 较短的文本

类型：

1. `char(M)`：M 为最大字符数，取值范围在 0 ~ 255 之间的整数。为固定长的字符，效率高。M 可以省略，默认为1
2. `varchar(M)`：M 为最大字符数，取值范围在 0 ~ 65535 之间的整数。为可变长度的字符，效率低。M 不可以省略
3. `enum(list)`：枚举类型，要求插入的值必须属于列表中指定的值之一。如果列表成员数量为 1 ~ 255，则需要 1 个字节存储。如果列表成员数量为 255 ~ 65535，则需要2个字节存储。最多 65535 个成员
4. `set(list)`：集合类型，和枚举型类似，但最多保存 64 个成员。且集合类型可以一次插入多个成员，根据成员个数不同所占字节不同，每 8 个成员占一个字节，不满 8 个成员按 8 个成员计算，最多 8 字节。
5. `binary`、`varbinary`：用于保存较短的二进制数据

特点：

1. 固定长度字符，代表插入字符时，mysql 开辟的空间为你定义时的长度。可变长度字符表示插入字符时，mysql 开辟的空间为插入的字符实际长度，最大为你定义的长度
2. 枚举类型和集合类型插入时插入的成员不分大小写，写入后的数据和预设列表中的数据一致，且枚举类型每次插入只能选择列表中的一个成员，集合类型可以插入多个列表中的成员

```sql
CREATE TABLE tab_char(
   c1 ENUM('Leon','Bob','Tom'),
    c2 SET('a','b','c')
);

INSERT INTO tab_char
VALUES('leon','a'),
VALUES('BOB','A,b');
```

#### 较长的文本

### 日期型

1. `date`：占 4 字节，只保存日期，最小值为 1000-01-01，最大值为 9999-12-31
2. `time`：占 3 字节，只保存时间，最小值为 -838:59:59，最大值为 838:59:59
3. `year`：占 1 字节，只保存年份，最小值为 1901，最大值为 2155
4. `datatime`：占8字节，保存日期和时间，最小值为 1000-01-01 00:00:00，最大值为 9999-12-31 23:59:59
5. `timestamp`：占4字节，保存日期和时间，最小值为 1970-01-01 08:00:01，最大值为 2038 年某个时间

特点：

1. `timestamp` 和实际时区有关，更能反映实际的日期，而 `datetime` 则只能反映出插入时的当地时区
2. `timestamp` 的属性受 MySQL 版本和 SQLMode 的影响较大

## 常见约束

含义：一种限制，用于限制表中的数据，为了保证表中的数据的准确和可靠性。一个列可以添加多个约束，用空格隔开。

分类：

1. `not null`：非空，用于保证该字段的值不能为空
2. `default`：默认，用于该字段有默认值
3. `primary key`：主键，用于保证该字段的值具有唯一性，并且非空，一个表中最多一个，可以组合但不推荐。
4. `unique`：唯一，用于保证该字段的值具有唯一性，可以为空，一个表中可以多个，可以组合但不推荐。
5. `check`：检查约束，MySQL 中不支持
6. `foreign key`：外键，用于限制两个表的关系，用于保证该字段的值必须来自于主表的关联列的值。
   1. 在从表添加外键约束，用于引用主表中某列的值。

   2. 从表的外键列的类型和主表的关联列的类型要求一致或兼容，名称无要求

   3. 主表的关联列必须是一个 key（一般时主键或唯一键）

   4. 插入数据时，应该先插入主表，再插入从表。删除时应先删除从表，再删除主表

   5. 可以通过设置级联删除或级联置空，直接删除主表中和外键关联的数据

      > 关键字：`ON DELETE CASCADE|SET NULL`
      >
      > 设置级联删除：`ALTER TABLE 表名 ADD CONSTRAINT 外键名 FOREIGN KEY(从表列名) REFERENCES 主表名(主表被引用列名) ON DELETE CASCADE;`
      >
      > 设置级联置空：`ALTER TABLE 表名 ADD CONSTRAINT 外键名 FOREIGN KEY(从表列名) REFERENCES 主表名(主表被引用列名) ON DELETE SET NULL;`
      >
      > Tips：设置后，当直接删除主表中和外键关联的数据时，从表中关联的数据会被删除或置空

添加约束的时机：

1. 创建表时
2. 修改表时

约束的添加分类

1. 列级约束：六大约束语法上都支持，但外键约束没有效果
2. 表级约束：除了非空、默认，其他的都支持

### 创建表时添加约束

1. 添加列级约束

   语法：直接在字段名和类型后面追加约束类型即可，只支持默认、非空、主键、唯一

   ```sql
   USE students;
   CREATE TABLE stuinfo(
      id INT PRIMARY KEY,  #主键
       stuName VARCHAR(20) NOT NULL,   #非空
       gender CHAR(1) CHECK(gender='男' or gender='女'), #检查
       seat INT UNIQUE, #唯一
       age INT DEFAULT 18  #默认
   )
   ```

2. 添加表级约束

   语法：在各个字段的最下面 `[constraint 约束名] 约束类型(字段名)`

   ```sql
   CREATE TABLE stuinfo(
      id INT,
       stuName VARCHAR(20),
       gender CHAR(1),
       seat INT,
       age INT,
       majorid INT,

       CONSTRAINT pk PRIMARY KEY(id),  #主键
       CONSTRAINT uq UNIQUE(seat),  #唯一键
       CONSTRAINT ck CHECK(gender = '男' or gender = '女'), #检查
       CONSTRAINT fk_stuinfo_najor FOREIGN KEY(majorid) REFERENCES major(id)  #外键
   );
   ```

### 修改表时添加约束

语法：

1. `ALTER TABLE 表名 MODIFY COLUMN 列名 列类型 列级约束;`
2. `ALTER TABLE 表名 ADD [CONSTRAINT 约束名] 表级约束(列名) [外键的引用];`

```sql
#添加非空约束
ALTER TABLE stuinfo MODIFY COLUMN stuname VARCHAR(20) NOT NULL;

#添加默认约束
ALTER TABLE stuinfo MODIFY COLUMN age INT DEFAULT 18;

#添加主键
#1.列级约束
ALTER TABLE stuinfo MODIFY COLUMN id INT PRIMARY KEY;
#2.表级约束
ALTER TABLE stuinfo ADD PRIMARY KEY(id);

#添加唯一键
#1.列级约束
ALTER TABLE stuinfo MODIFY COLUMN seat INT UNIQUE;
#2.表级约束
ALTER TABLE stuinfo ADD UNIQUE(seat);

#添加外键约束
ALTER TABLE stuinfo ADD CONSTRAINT fk_stuinfo_major FOREIGN KEY(majorid) REFERNCES major(id);
```

### 修改表时删除约束

```sql
#删除非空约束
ALTER TABLE stuinfo MODIFY COLUMN stuname VARCHAR(20) NULL;

#删除默认约束
ALTER TABLE stuinfo MODIFY COLUMN age INT;

#删除主键
ALTER TABLE stuinfo DROP PRIMARY KEY;

#删除唯一键
ALTER TABLE stuinfo DROP INDEX seat;

#删除外键约束
ALTER STUINFO DROP FOREIGN KEY fk_stuinfo_major;
```

## 标识列

关键字：`auto_increment` 放在约束后。

含义：又称为自增长列，可以不用手动插入值，系统提供默认的序列值

特点：

1. 标识列必须可一个 key 搭配使用，不一定是主键
2. 一个表至多有一个标识列
3. 标识列的类型只能是数值型
4. 标识列可以通过 `set auto_increment_increment=num` 设置步长，也可以通过手动插入值设置起始值。
