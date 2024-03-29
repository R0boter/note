
## 常见术语

1. DB：数据库(database)，存储数据的仓库，它保存了一系列有组织的数据

2. DBMS：数据库管理系统(Database Management System),数据库是通过DBMS创建和操作的容器

   > 常见的DBMS有：MySQL、Oracle、DB2、SqlServer、Access
   >
   > **DBMS**分为两类：
   >
   > > 1. 基于文件共享系统的DBMS(Access)
   > >
   > > 2. 基于C/S(客户端/服务端)架构的DBMS(MySQL、Oracle、SqlServer)
   >
   > SQL:结构化查询语句(Structure Query Language),专门用来与数据库进行通信的语言
   > **优点：**
   >
   > 1. 通用性，几乎所有的DBMS都支持SQL
   >
   > 2. 简单易学
   >
   > 3. 强有力的语言，灵活使用了其他的语言元素，可以进行非常复杂和高级的数据库操作
   >
   >    **Tips：三者之间的关系为：DBMS通过SQL管理DB**

## 数据库结构

1. 数据库由库、表、列、值组成
2. 一个数据库可以包含多个表，每个表有相应的表名用来标识该表，表名具有唯一性
3. 表具有一些特性，这些特性定义了数据在表中是如何存储的，类似于JAVA中的'类'
4. 表由列组成，也称为字段，所有的表都是由一个或多个列组成，每一列类似于JAVA中的'属性'
5. 表中的数据是按照行进行存储的，每一行类似于JAVA中的'对象'

## 关于MySQL的一点基础知识

* 新版MySQL安装后需要初始化
  
  1. 初始化命令： `sudo mysqld --initialize --user=mysql --basedir=/usr --datadir=/var/lib/mysql`
  2. 注意初始化后的输出会显示默认生成的登陆密码
  3. 登陆命令: `mysql -uroot -p`
  4. 修改默认密码： `ALTER USER 'root'@'localhost' identified by '123456'`

* MySQL有两种版本：企业版(收费)、社区版(免费)

* 在MySQL中字符集为utf8,而不是utf-8

* MySQL的配置文件MySQL安装目录下的my.ini

* windows命令行下MySQL服务的启动和停止是：`net start(stop) MySQLname`

* MySQL的登陆与退出有两种方式：

  > 1. 通过自带的客户端(仅限于root用户)
  > 2. 通过命令行登录：mysql \[-h 主机名 -P 端口] -u 用户名 -p密码
  >
  > **Tips:**
  >
  > > 1. 本机登录可以省略主机名和端口号，mysql默认的端口号为3306
  > > 2. -p后不输入密码则会要求星号输入密码，如果在-p后输入密码，-p和密码中间不能存在空格
  > > 3. 要在windows命令行下直接运行mysql需要将安装目录下的bin文件夹添加到环境变量里面

* 退出：`exit`和`ctrl+c`

## SQL 语句的基本规范和简单的常用命令

SQL语句的语法规范：

> 1. SQL语句是以分号或\g结尾(建议使用分号)
>
> 2. SQL语句不区分大小写，但建议关键字大写，表名、列名使用小写
>
> 3. 根据命令需要进行缩进或换行
>
> 4. 注释：分为单行注释和多行注释
>
> > 单行注释：使用`#`或`--空格`
> >
> > 多行注释：使用/\*注释文字*/

## MySQL基本库

当**MySQL**创建好后会又四个默认数据库

> Information_schema：    保存元数据信息
>
> Mysql：                            保存用户信息
>
> Performance_schema：    收集性能信息和性能参数
>
> Test：                                测试数据库(可删除)

## 常用的简单命令

显示当前数据库：`show databases;`

进入数据库：`use 库名;`

显示当前数据库的所有表：`show table;`

显示其他数据库的表：`show table from 库名;`

查询当前所在库名：`select database();`

创建表：

```sql
creat table 表名(
    列名 列类型，
    ......,
    列名 列类型
    );
```
