# python基础

## Python简介

1. Python是一种解释性、面向对象、动态数据类型的高级程序设计语言，遵循GPL(GNU General Public License)协议

   > 解释型：不需要编译
   >
   > 交互式：可以在一个Python提示符，直接互动执行程序
   >
   > 面型对象：Python支持面相对象的风格或代码封装在对象的编程技术
   >
   > 初学者语言：支持广泛的应用程序开发，从文字处理到浏览器带游戏

2. 特点:

   > 易于学习：较少的关键字、结构简单、明确定义的语法
   >
   > 易于阅读：Python代码定义的更清晰
   >
   > 易于维护：Python的成功在于它的源代码容易维护
   >
   > 广泛的标准库：Python具有丰富的库，跨平台的，在UNIX、Windows和Macintosh
   >
   > 可移植性：基于开源的特性，Python已经被移植到其他平台
   >
   > 可扩展性：可以使用C和C++完成部分程序，然后从Python程序中调用
   >
   > 数据库：Python提供所有的商业数据库的接口
   >
   > GUI编程：Python支持GUI可以创建和移植到许多系统调用
   >
   > 可嵌入：可以将Python嵌入到C/C++程序，让程序的用户获得“脚本化”的能力

3. Python文件的头注释(Shebang)

```python
   #!/usr/bin/env python        #在Linux下使用chmod命令赋予可执行权限后可以直接运行py文件,这里是给程序指定了解释器的路径
   # -*- codding: utf-8 -*-                        #指定py文件的编码格式
   # @Author: xxxx                                #作者名
   # @Date: xxxx-xx-xx xx:xx:xx                    #创建时间
   # @Last Modified by: xxxx                        #最后修改者
   # @Last Modified time: xxxx-xx-xx xx:xx:xx    #最后修改时间
```

## 注释

1. 单行注释：Python使用`#`做为单行注释符
2. 多行注释：Python使用三个单引号或双引号做为多行注释(前后各三个)

## 基本输入与输出

1. 输出：`print`作为Python的输出函数。

   > 1. **print**可以输出数字，字符串，表达式以及其他数据类型，如果输出字符串，需加单引号或双引号
   >
   > 2. 如果输出的数据有多行，可以使用`'''`(三引号)保留输出格式

2. 输入：`input`作为Python的输入函数,input默认输入的是String型数据，如果要保证输入的是其他类型需要强制转换

   ```python
      age = input()
      print("age = ", age)
      # 或
      age = input("请输入你的年龄")
      print("你的年龄是：", age)
      # 将转换input输入的值转换为整型
      num1 = int(input("请输入第一个数字"))
      num2 = int(input("请输入第二个数字"))
      print(“num1 + num2 =”, num1 + num2)
   ```

3. 格式化输出
    占位符：int型`%d`、浮点型`%f`、字符型`%s`

    格式：

   ```python
      num = 123
      str1 = "Leon is me"
      f = 10.23
      print("num = %d,str1 = %s,f = %.2f" % (num.str1,f))
   ```

   > Tips:
   >
   > 浮点型可指定保留小数点后n位，格式为`%.nf`。会四舍五入
   >
   > 换行符:`\n`
   >
   > 制表符:`\t`
   >
   > 转义符:`\`
   >
   > 如果一个字符串中有多个字符需要转义，Python中可使用r表示该字符串默认不转义
   >
   > 格式为:`print(r"E:\nearn\took")`

## 迭代

1. 可迭代对象(Iterable)

   > 定义:可以直接作用于for循环的对象，统称为可迭代对象(Iterable)
   > Iterable分为两种:
   >
   > 1. 集合类的数据类型，如：string,list,tuple,dict,set
   > 2. generator(生成器)，包括：生成器和包含yield的generator function

2. 判断是否是可迭代对象

   ```python
      # 需先导入collections包中的Iterable
      from collections import Iterable
      # 使用isinstance()方法判断，以下都为Ture
      print([],Iterable)
      print((),Iterable)
      print("",Iterable)
      print({},Iterable)
      print((x for x in range(10)),Iterable)
   ```

3. 迭代器(Iterator)

   > 定义:不但可以作用于for循环，还可以被next()函数不断调用并返回下一个值的对象，被称为迭代器(Iterator对象)
   > Tips:next()函数会不断调用Iterator对象，并返回下一个值，直到最后抛出一个StopIteration错误表示无法继续返回下一个值

4. 判断是否是迭代器对象

   ```python
   # 需先导入collections包中的Iterator
   from collections import Iterator
   # 使用isinstance()方法判断，以下都为False
   print([],Iterable)
   print((),Iterable)
   print("",Iterable)
   print({},Iterable)
   # 以下为Ture,(x for x in range(number))会返回一个Iterator
   print((x for x in range(number)),Iterable)
   print((x for x in list,Iterable)
   # 利用iter()可以将Iterable转为Iterator
   iterator1 = iter([1, 2, 3])
   iterator1 = iter((1, 2, 3))
   iterator1 = iter({1:"a", 2:"b", 3:"c"})
   iterator1 = iter("abc")
   next(iterator1)
   ```
