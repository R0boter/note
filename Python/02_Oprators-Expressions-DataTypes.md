
## 运算符与表达式

表达式：由变量、常量和运算符组成的式子

1. 算数运算符与算数运算表达式

   | +   | -   | *   | /   | %    | **   | //   |
   | --- | --- | --- | --- | ---- | ---- | ---- |
   | 加  | 减  | 乘  | 除  | 取模 | 求幂 | 取整 |

   > 功能：进行相关符号的数学运算，不会改变变量的值
   >
   > 值：相关数学运算结果

2. 赋值运算符和赋值运算表达式

   > 运算符：=
   >
   > 格式：变量 = 表达式
   >
   > 功能：计算了运算符右侧的表达式的值，并赋值给运算符左侧的变量
   >
   > 值：赋值结束后变量的值

3. 复合运算符

   > 运算符：+=、-=等，即算数运算符和赋值运算符的组合
   >
   > 格式：a+=b
   >
   > 功能：相当于将a与b的值相加后再赋值给a

4. 位运算符

   > 概念：位运算符是将数字看作二进制来进行运算的
   >
   > 运算符：
   >
   > `&`按位与：当两个数字的同一个二进制位都为1时，则结果为1。反之，为0
   >
   > `|`按位或：当两个数字的同一个二进制位有一个为1时，结果为1。反之，为0
   >
   > `^`按位异或：当两个数字的同一个二进制位相异时，结果为1。反之，为0
   >
   > `~`按位取反：一个数字的每一个二进制位取反
   >
   > `<<`左移位：一个数字的所有二进制位向左移动若干位，由`<<`右侧的数字决定移动位数，高位丢弃，低位补0
   >
   > `>>`右移位：一个数字的所有二进制位向右移动若干位，由`>>`右侧的数字决定移动位数，低位丢弃，高位补0

5. 关系运算符

   | ==   | !=     | >    | <    | >=       | <=       |
   | ---- | ------ | ---- | ---- | -------- | -------- |
   | 等于 | 不等于 | 大于 | 小于 | 大于等于 | 小于等于 |

   > 格式：表达式1 关系运算符 表达式2
   > 功能：计算两侧表达式的值，并进行比较
   > 值：如果关系成立，则结果为真，反之，为假

6. 逻辑运算符

   > 逻辑与：`表达式1 and 表达式2`。当两个表达式中有一个值为假，则结果为假
   >
   > 逻辑或：`表达式1 or 表达式2`。当两个表达式中有一个值为真，则结果为真
   >
   > 逻辑非：`not 表达式`。当表达式的值为真，则结果为假。反之，则为真
   >
   > 短路原则：在逻辑与和逻辑非中，如果有多个表达式，当前面的表达式有值为假或有值为真时，则不再计算后面的值

7. 成员运算符

   > `in`：如果在指定的序列中找到值，则返回Ture，否则返回False
   >
   > `not in`：如果在指定的序列中没有找到值，则返回Ture，否则返回False

8. 身份运算符

   > `is`：判断两个标识符是否引用的同一个对象
   >
   > `is not`：判断两个标识符是否引用的不同的对象

9. 运算符优先级(自上而下)

```python
**
~    +    -    （这里是正负号，即一元运算符）
*    /    %    //
+    -    (这里是加减号)
>>    <<
&
^    |
>    <    >=    <=
==    !=
=    %=    +=    -=    //=
is    is not
in    not in
not    or    and
```

## Number型

1. 整型：可以处理任意大小的数字，包括负整数，在程序中表示方法和数学写法一样

   > 连续定义多个变量：num1 = num2 = num3 =1
   >
   > 交互式赋值定义变量：num4, num5 = 3, 4

2. 浮点型：由整数和小数部分组成，浮点数运算存在四舍五入的误差问题

3. 复数型：由实数部分和虚数部分构成

   ```python
   # 强制类型转换
   # 浮点数转为整数，向下取整
   print(int(1.9))        # 输出结果为1
   # 整数转为浮点数
   print(float(1))        # 输出结果为1.0
   # 字符串转整数或浮点数
   print(int("123"))    # 输出结果为123
   print(float("123"))    # 输出结果为123.0
   # +和-只有作为正负号才有效
   print(int("-123"))    # 输出结果为-123
   print(int("12-3"))    # 报错
   # 如果字符串中存在无效字符，则报错
   print(int("asdf"))    # 报错
   ```

4. 数学function：

   ```python
   abs()                    # 求绝对值
   (a > b)- (a < b)         # 比较两个数的大小，返回1表示 a 大于 b ,返回 -1 表示 a < b
   max(num1,num2,num3,....)        # 返回给定参数的最大值：
   min(num1,num2,num3,....)        # 返回给定参数的最小值
   pow( x, y)            # 求x的y次方
   round(x, [n])         # 返回浮点数x的四舍五入的值，如果给定n值，则代表舍入到小数点后n位

   # import是导入库（封装的一些功能），math库：数学相关库
   import math
   # 向上取整
   print(math.ceil(18.1))        # 结果为19
   # 向下取整
   print(math.floor(18.9))    # 结果为18
   # 返回小数部分和整数部分，结果都为浮点数
   print(math.modf(22.3))        # 结果为（0.3000000007，22.0）
   # 开方，返回的浮点数
   print(math.sqrt(16))        # 结果为4.0
   ```

5. 随机数

   ```python
   import random
   print(random.choice(list))        # 从列表中随机取一个元素
   print(random.choice(range(5)))    # range(5) == [0,1,2,3,4]
   print(random.choice("sun"))        # "sun" == ["s","u","n"]
   # random.randrange([start],stop,[step]),从指定范围内，按指定的基数递增的集合中选取一个随机数，包含start值，不包含stop值
   print(random.randrange(1,100,2))
   print(random.random())            # 随机产生0-1之间的浮点数，包含0不包含1
   print(random.uniform(3,9))        # 随机产生3-9之间的实数，包含3和9
   # random.shuffle()将列表内的元素进行随机排列
   list=[1,2,3,4,5]
   random.shuffle(list)
   print(list)
   ```

## String型

1. 定义

   > 概念：字符串时以单引号或双引号括起来的任意文本，且字符串不可变
   > 创建：`str1 = "leon is me!"`
   > Tips：list中元素的访问速度会随着数据的增多而变慢，但比dict占用内存小

2. 字符串运算：

   ```python
   #字符串的连接
   str1 = "Leon is"
   str2 = "me"
   str3 = str1 + str2
   print("str3=",str3)
   #输出重复的字符串
   str4 = "good"
   str5 = str4 * 3
   print(str5)
   ```

3. 访问字符串中指定的元素

   通过索引下标查找的字符串中的单个元素，索引从0开始

   格式：`字符串名[下标]`

   ```python
   #打印该字符串中的o
   str1 = "leon is me!"
   print(str1[2])
   ```

4. 字符串截取

   格式：`字符串名[start：stop]`

   start为指定开始的下标，stop为指定结束的下标，可不写，默认为第一位和最后一位，截取后的字符串包含start，不包含stop

   ```python
    str1 = "Leon is me"
    #取出 is
    str2 = str1[5:7]
    #取出 Leon
    str3 = str1[:4]
    #取出 me
    str4 = str1[8:]
   ```

5. 成员运算符的运用

   ```python
   str1 = "Leon is me"
   # 判断Leon是否存在str1中，存在返回True，不存在返回False
   print("Leon" in str1)
   # 判断Leon1是否不存在str1中，不存在返回True，存在返回False
   print("Leon1" not in str1)
   ```

6. 字符串比较

   > 规则：从字符串第一位字符开始比较，谁的ASCII码大，谁就大。如果相等则比较第二位。如果长度不一样，则在没有的那一位用`\0`代替

7. 一些常用的对str进行操作的方法

   ```python
   str.lower():            # 将字符串中的大写字母转换为小写字母
   str.upper():            # 将字符串中的小写字母转换成大写字母
   str.swapcase():            # 将字符串中的大写转为小写，小写转为大写
   str.capitalize():        # 将字符串中第一个单词的首字母大写，其他小写
   str.title()：            # 将字符串中每个单词的首字母大写，其他小写
   str.center(width,"fillchar")：    # 返回一个指定width宽度的字符串，两侧用fillchar指定的字符填充
   str.ljust(width[,"fillchar"])：    # 返回一个指定width宽度的左对齐的字符串，右侧用fillchar指定的字符填充
   str.rjust(width[,"fillchar"])：    # 返回一个指定width宽度的右对齐的字符串，左侧用fillchar指定的字符填充
   str.zfill(width)：    # 返回一个指定width宽度的右对齐的字符串，左侧用0补齐
   str1.count("str2"[,start][,end])：    # 返回str1字符串中str2字符串出现的次数，可以利用元素下标指定查找范围，默认从头到尾
   str1.find("str2"[,start][,end])：    # 从左至右检查str1中是否包含str2，包含就返回str2第一次出现时的下标，不包含就返回-1.可以利用元素下标指定查找范围
   str1.rfind("str2"[,start][,end])：    # 从右至左检查str1中是否包含str2，包含则返回str2第一次出现时的下标，反之返回-1，可以利用元素下标指定查找范围
   str1.index("str2"[,start][,end])：    # 从左至右在str1中查找str2并返回str2的下标，可以利用元素下标指定查找范围。不包含会报异常
   str1.rindex("str2"[,start][,end])：    # 从右至左在str1中查找str2并返回str2的下标，可以利用元素下标指定查找范围。不包含会报异常
   str.lstrip("fillchar")：        # 截取掉左侧fillchar指定的字符，默认为空格(即不指定)
   str.rstrip("fillchar")：        # 截取掉右侧fillchar指定的字符，默认为空格
   str.strip("fillchar")：        # 截取掉两侧fillchar指定的字符，默认为空格
   str.split("char"[,num])        # 以指定的char为分隔符，截取字符串并返回一个list，num为指定截取多少个字符串，默认为len(str)
   str.splitlines([bool])        # 以['\r','\r\n',\n]中的一种为分隔符，截取字符串并返回一个list，bool值默认为false，如果指定为ture，则截取后的字符串会保留\n
   "str".join(seq)                # 以指定的str为分隔符，将指定seq中元素拼接成一个字符串。注意：str可以为空，seq为任何序列，例如str,list,tuple。如果seq为list或tuple,那么需要将list或tuple中的数字也转换成str型才能拼接
   str.replace("oldstr","newstr",count)    # 用newstr替换str中的oldstr，count指定替换次数，默认是全部
   str1.startswith("str2"[, start][, end])    # 判断指定的范围内是否是用指定的str2做为开头的，start默认为0，end默认为len(str2)
   str1.endswith("str2"[, start][, end])    # 判断指定的范围内是否是用指定的str2做为结尾的，start默认为0，end默认为len(str2)
   str.encode(["encoding"][, "errors"])    # 对str进行编码，encoding为指定的编码格式，默认为utf-8。errors为指定对错误的处理方式，默认为strict,实际上常用的为ignore(忽略错误)，编码后的数据类型为bytes型
   bytes.decode("encoding", "errors")        # 对bytes进行解码，encoding为指定的解码格式，必须和编码格式一致，否则会出现乱码或报错。errors为指定对错误的处理方式，常用为ignore(忽略错误)。decode()方法在python3中只存在于bytes类型中
   str.isalpha()    # 如果str不为空，且所有字符都是字母，则返回Ture,反之False
   str.isfigit()    # 如果str不为空，且所有字符都是数字，则返回Ture，反之False
   str.isnumeric()    # 如果str不为空，且所有字符都是数字，则返回Ture，反之False
   str.isalnum()    # 如果str不为空，且所有字符都是数字或字母，则返回Ture，反之，则返回False
   str.isupper()    # 如果str中至少有一个英文字符，且所有英文字符都是大写的英文字母，则返回Ture,反之，则返回False
   str.islower()    # 如果str中至少有一个英文字符，且所有英文字符都是小写的英文字母，则返回Ture,反之，则返回False
   str.istitle()    # 如果str是标题化，即所有单词首字母为大写，则返回Ture,反之，则返回False
   str.isdecimal()    # 如果str不为空，且只包含十进制字符，则返回Ture，反之False
   str.isspace()    # 如果str只包含空白符，则返回Ture,反之False
   ord("str")        # 将字符转为ASCII码
   chr("ASCII")    # 将ASCII码转为字符
   max(str)        # 返回字符串中最大值，以ASCII码值进行比较
   min(str)        # 返回字符串中最小值，以ASCII码值进行比较
   eval(str)：        # 将字符串str当成有效的表达式来求值并返回计算结果
   num1 = eval("123")
   num2 = eval("1+23")
   len(str)：        # 返回字符串的长度
   str1 = "leon is me"
   print(len(str1))
   ```

## Boolean型和None

1. Boolean(布尔值)：

   > True：真
   > False：假

2. None(空值)：

   > 空值在Python中是一个特殊的值，用None表示，但None不能表示为0，因为0是有意义的，而None是无意义的特殊值

## List型

1. 定义：列表是一个有序的集合

2. 格式：`列表名 = [列表选项1, 列表选项2, ......, 列表选项n]`

   > Tips：
   >
   > 1. 可以创建空列表`列表名 = []`
   > 2. 列表中的元素不一定是同一种类型`列表名 = [1, "Leon", True]`

3. 取值与替换：`列表名[下标]`。注意：不能越界

4. 列表的运算

   ```python
   # 列表的拼接
   list1 = [1, 2, 3]
   list2 = [4, 5, 6]
   list3 = list1 + list2
   # 列表的重复
   list1 = [1, 2, 3]
   list2 = list1 * 3
   # 成员运算符的使用
   list1 = [1, 2, 3, 4, 5]
   print(3 in list1)            # 存在输出True,反之,输出False
   print(6 not in list1)        # 不存在输出True,反之,输出False
   ```

5. 列表的截取

   格式：`列表名[start：stop]`

   start为指定开始的下标，stop为指定结束的下标，可不写，默认为第一位和最后一位，截取后的字符串包含start，不包含stop

   ```python
   list1 = [1, 2, 3, 4, 5]
   list2 = list1[1:4]
   list3 = list1[:3]
   list4 = list1[2:]
   ```

6. 嵌套

   ```python
   # 列表中的元素也可以是列表
   list1 = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
   # 通过列表下标进行访问与修改
   num1 = list1[1][2]
   list1[0][2] = 7
   ```

7. 引用

   ```python
   # 引用
   list1 = [1, 2, 3]
   list2 = list1
   # 修改list2中的元素的值时，list1中元素的值也会随之改变
   list2[1] = 5
   print(list1, list2)
   ```

8. 常用方法

   ```python
   # list.append(element)                在列表末尾追加一个元素
   list1 = [1, 2, 3]
   list1.append(4)
   list1.append([4,5,"Leon"])    # 这个追加的列表将作为原列表中的一个元素
   list.extend([element, element])    # 在列表末尾追加另一个列表的多个值,无追加单个元素
   list1 = [1, 2, 3]
   list1.extend([4, 5, "Leon"])
   # list.insert(index,element)            在指定的下标处(index)添加指定的元素(element),原数据向后顺延一位
   list1 = [1, 2, 3]
   list1.insert(1,5)
   list1.insert(1,[4, 5, 7])
   # list.pop(index)                    移除指定下标处的元素，默认删除最后一位，并返回删除的数据
   # list.remove(element)                移除列表中匹配到的第一个元素
   # list.clear()                        清除列表中的所有元素
   # list.index(element,[start],[stop])    返回所查找列表中指定范围中匹配到的第一个元素的下标，不指定范围则为列表中第一个匹配到的元素下标
   # len(list)                            查看列表中的元素个数
   # max(list)                            返回列表中的最大值,列表中只能全是Number型
   # min(list)                            返回列表中的最小值,列表中只能全是Number型
   # list.count(element)                返回指定元素在列表中出现的次数
   # list.reverse()                        将列表倒序
   # list.sort()                        返回将列表升序排序后的列表
   # list.copy()                        拷贝列表，拷贝后的列表和原列表占用的内存不一样。区别于引用
   # list(tuple_name)                    将元组转换成列表
   # list(set_name)                    将set转换成list
   ```

## Tuple型

1. 定义：与list相似的一种有序的集合,但tuple与list的区别就在于其不可变的安全性

   特点：

   > 1. 使用小括号
   > 2. 一旦初始化就不能修改

2. 格式：

   ```python
   # 创建一个空tuple
   tuple1 = ()
   # 创建一个带元素的tuple,tuple型可以包含不同类型的元素
   tuple2 = (1, "Leon", True)
   # 创建单个元素的tuple,必须带逗号
   tuple3 = (1,)
   ```

3. tuple元素的访问格式为：tuple_name[index]

   ```python
   # index的值从0开始
   tuple1(1, 2, 3, 4, 5)
   print(tuple1[0])
   print(tuple1[4])
   # 逆向获取元素
   print(tuple1[-1])            # 逆向获取最后一位元素的值
   print(tuple1[-5])            # 逆向获取第一位元素的值
   # 不能越界
   print(tuple1[5])            # 正向越界
   print(tuple1[-6])            # 逆向越界
   ```

4. tuple的修改与删除

   ```python
   # tuple的元素不能修改，但如果tuple中的元素类型为可修改的，那么可以修改tuple元素中的元素
   tuple1 = (1, 2, [3, 4, 5])
   tuple1[2] = [7, 8, 9]            # 报错，tuple中的元素无法修改
   tuple1[2][1] = 6                # 可以，因为list中的元素可以修改
   # del是将tuple删除，不是清空,删除后无法再使用tuple1
   del tuple1
   ```

5. tuple的运算

   ```python
   # 拼接
   tuple1 = (1, 2, 3)
   tuple2 = (4, 5, 6)
   tuple3 = tuple1 + tuple2
   # 重复
   tuple1 = (1, 2, 3)
   print(tuple1 * 3)
   # 判断元素是否在tuple中
   tuple1 = (1, 2, 3)
   print(3 in tuple1)
   ```

6. tuple的截取

   格式：`tuple_name[start：stop]`

   start为指定开始的下标，stop为指定结束的下标，可不写，默认为第一位和最后一位，截取后的字符串包含start，不包含stop

   ```python
   tuple1 = [1, 2, 3, 4, 5]
   tuple2 = tuple1[1：4]
   tuple3 = tuple1[：3]
   tuple4 = tuple1[2：]
   ```

7. 二维tuple：元素为一维tuple的tuple

8. 常用方法：

   ```python
   len(tuple_name)        # 返回tuple中元素的个数
   max(tuple_name)        # 返回tuple中的最大值
   min(tuple_name)        # 返回tuple中的最小值
   tuple(list_name)    # 将list转换成tuple
   tuple(set_name)        # 将set转换成tuple
   ```

## Dict型

1. 概述： 使用键-值对(key--value)进行存储

   > 创建：
   > 格式：dict_name = {key：value,key：value}
   > key的特性：
   >
   > 1. 字典中的key必须是唯一的
   > 2. key必须是不可变对象，例如str型和number型不可变可以作为key，list可变，不能作为key
   >
   > Tips1：dict是无序的，具有极快的访问速度，不会随数据的增加降低效率,但占用大量内存。
   >
   > Tips2：可以创建空字典

2. 增删改查：

   > 增加：dict_name[new_key] = value
   > 更改：dict_name[old_key] = new_value
   > 删除：dict_name.pop(key)
   > 访问：dict_name[key]
   > 如果所访问的key不存在dict中，会产生报错。所以常用下面的方法访问
   > 访问：dict_name.get(key)
   > 使用第二种方法访问，当key不存在dict中时会返回None,不会报错

3. 四种遍历方法

   ```python
   # 使用key进行遍历
   for key in dict_name：
       print(key,dict_name[key])
   # 使用value进行遍历,dict_name.values()是将dict中所有value返回为一个list
   for value in dict_name.values()：
       print(value)
   # 使用dict.items()进行遍历，dict.items()是将dict返回为一个list，dict中的每一个key-value对返回为一个tuple，作为list的一个元素
   for k, v in dict_name.items()：
       print(k, v)
   # 使用enumerate(dict)进行遍历，enumerate(dict)是为dict中的key进行排序，利用下标进行遍历
   for i, k in enumerate(dict_name)：
       print(i, k)
   ```

## Set

1. 定义：一组不可变也不可重复的元素的无序集合，类似于dict

2. 创建：

   ```python
   set1 = {element1,element2,element3}
   set1 = set(seq)
   # seq可以为str,list,tuple或dict，当dict作为seq输入时，只会取dict中的key，不会取value
   # 当seq为str或list或tuple时，set会自动去重
   ```

3. 添加：`set_name.add(new_element)`

   > 1. new_element必须是不可变类型，list和dict都不能作为new_element。因为list中的元素是可变，dict中value元素也是可变的，而num,str,tuple可以作为new_element
   > 2. new_element可以与set中已存在的element重复，但添加后set会自动去重

4. 更新：`set_name.update(new_element)`

   > 1. 更新的作用和添加是一样的，但它可以添加list和dict
   > 2. 更新是将new_element打碎后插入到set中

5. 删除：`set_name.remove(element)`

6. 交集与并集

   ```python
   # 交集,返回两个set中一样的element
   set1 = set2 & set3
   # 并集,将两个set合并去重，并返回
   set1= set2 | set3
   ```

7. 类型转换

   ```python
   # set更多的是用于数据的去重，通过将其他类型转换成set去重后，再转换为原类型
   set(list_name)    # 将list转换为set
   set(tuple_name)    # 将tuple转换为set
   ```

## Function

1. 本质：function是对某种功能的封装

2. 优点：

   > 1. 简化代码结构，增加代码的重复可利用性
   > 2. 如果要修改某些功能或BUG，只需修改对应的function即可

3. 定义function

   ```python
   def function_name(parameter_list)：
   语句
   return 表达式`
   ```

   > `def`：函数代码块以`def`关键字开始
   > `function_name`：遵循标识符命名规则
   > `()`：parameter_list的开始和结束
   > `parameter_list`：`(parameter1,parameter2,......,parameter_n)`形参列表。任何传入函数的参数和变量必须放在小括号中，用逗号隔开。参数是函数从函数调用者那里获取的信息
   > `:`：函数内容(即封装的功能)以冒号开始，并且缩进
   > `语句`：函数封装的功能
   > `return`：用于结束函数，并返回信息给函数的调用者
   > 表达式：即返回给函数调用者的信息
   > Tips：最后的`return 表达式`可以不写，相当于`return None`

4. 函数的调用：`function_name(argument_list)`

   > function_name：即要封装了要使用的功能的函数的函数名
   > argument_list：实参列表。函数调用者传递给函数的信息
   > Tips：函数调用的本质即，实参给形参赋值的过程

5. 参数：

   ```python
   # parameter(形式参数)：定义函数时小括号中的变量，本质是变量
   def myPrint(name,age)：
       print("Now %s is %d years old" % (name, age))
   # argument(实际参数)：调用函数时传递的数据，本质是值
   myPrint("Leon",20)
   # Tips：parameter和argument要按顺序传递，个数要对应
   # 默认参数，在定义function时，给parameter指定默认的参数，则在传递参数时个数不需要对应。注意：默认参数最好放在最后，否则在传参时只能使用关键字参数
   def myPrint1(name, age = 20)
   # 关键字参数，在传递参数时指定该argument传递给哪一个parameter，则不需要按顺序传递
   myPrint1(age = 20, name = "Leon")
   ```

   > 参数的传递：
   >
   > 1. 值传递：传递的不可变类型，如：number、string、tuple
   > 2. 引用传递：传递的可变类型,如：list、dict、set

6. 不定长参数：

    概念：能处理比定义时更多的参数

    格式：在定义function时，在parameter前添加`*`

   > 1. 添加单个星号，是生成一个tuple用来存放所有未命名的变量参数，如果在函数调用时没有指定参数，它就是一个空元组
   > 2. 添加两个星号，是生成一个dict用来存放所有未命名的变量参数，调用函数时传入的argument应该是以键值对的方式传入。如：`x=y`。

7. 返回值：

   ```python
   def mySum(num1,num2)：
       # 将结果返回给函数的调用者
       return num1 + num2
       # 执行完return后，函数结束。所有下面的语句不会执行
       print("****************")
   res = mySum(1, 2)
   print(res)
   ```

8. 匿名函数

   概念：不使用def语句来创建function，使用lambda来创建function

   特点：

   > lambda只是一个表达式，所有代码都在一行内，函数体比较简单
   > lambda的主体是一个表达式，而不是代码块。只能在lambda表达式中封装简单的逻辑
   > lambda函数有自己的命名空间，且不能访问自有参数列表之外的或全局命名空间的参数
   > lambda虽然简单，但与c/c++中的内联函数不同

   格式：`lambda parameter_list：expression`

   ```python
   # 创建
   sum1 = lambda num1, num2：num1 + num2
   # 调用
   print(sum1(1,2))
   ```
