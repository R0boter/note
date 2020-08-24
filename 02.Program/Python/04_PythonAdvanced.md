# python 进阶

## Decorator(装饰器)

1. 概念:装饰器是一个闭包，把一个函数当作参数传入，然后返回一个替代版的函数。本质上就是一个返回函数的函数

   > 闭包：如果在一个内部函数里，对在外部作用域(但不是全局作用域)的变量进行引用，那么这个内部函数就是一个闭包。
   > 闭包 = 内部函数 + 定义函数时的环境

   ```python
   def outer():
       x = 1            # 局部变量
       def inner():    # 内部函数
           print(x)    # 引用了外部作用域的变量
       return inner    # inner是一个闭包
   ```

2. 格式:

   ```python
   def outter(function_name):
       def inner(*args, **kwargs):
           # 装饰功能的代码块
           pass
           function_name(*args, **kwargs)
       return inner
   # 调用装饰器
   @outter
   # 需要装饰的函数
   def function_name(parameter_list):
       pass
   # 调用装饰后的函数
   function_name(argument_list)
   ```

3. 解释：

   > 1. 使用不定长参数`*args`和`**keargs`是为了让装饰器成为一个通用的装饰器
   > 2. 当函数function_name传入outter()后调用inner()函数，function_name()的参数会传入到inner()的parameter_list中，因为inner()的parameter_list是由两种不定长参数组成，所以不管function_name()的argument_list传入的参数是什么类型都能接收，然后运行装饰功能的代码块，再调用function_name()，最后返回inner()，此时的inner()就是在原function_name()函数的基础上进行装饰后的函数
   > 3. 使用`@`是调用装饰器，放在需要调用的函数上，作用和`function_name = outter(function_name)`一样

## Partial function(偏函数)

1. 概念:对某个function的参数进行控制，返回一个新的function

2. 使用:使用的是`functools`这个模块中的partial方法

3. 格式:

   ```python
   # 导入functools对象或只引入partial方法，二者取一即可
   import functools
   from functools import partial
   # 传入一个function，重新指定一个参数的默认值
   new_function_name = functools.partial(function_name,parameter_name = new_value)
   # 调用新函数
   new_function_name(argment_list)
   ```

4. 示例:以python自带的int()函数为例

   ```python
   '''
       int()函数有两个参数，第一个参数为*args，作为接收调用者传入的需要转换的数据，第二个参数base，默认值为10。是用于指定传入的数据是哪种进制，现在使用偏函数将返回一个默认传入的数据为二进制数据
   '''
   from functools import partial
   int2 = functools.partial(int, base = 2)
   int2(125)
   ```

## Action scope(作用域)

1. 概念:变量的有效范围。程序的变量并不是在所有位置都可以使用，变量赋值时的位置决定了变量的访问权限

2. 类型:

   > 1. 局部作用域
   > 2. 全局作用域
   > 3. 内建作用域

## 异常处理

1. 作用:当程序执行中发生异常情况时，不让程序结束而继续往下执行

2. 格式:

   ```python
   # 默认方式
   try:
       语句0
   except 异常名称1 as variable:
       语句1
   except 异常名称2 as variable:
       语句2
   ......
   except 异常名称n as variable:
       语句n
   else:
       语句e
   ```

   > 1. 作用:用来检测`语句0`的错误，从而让except捕获错误信息并处理
   >
   > 2. 逻辑:当程序执行到`try...except...else`语句时，会检查语句0在执行时是否存在错误.
   >
   >    如果`语句0`出现错误，则会依次匹配`except`中的异常名称直到匹配成功并将异常信息赋值给`variable`并执行对应`except`语句下的语句(可直接打印variable,输出错误信息)。
   >
   >    如果`语句0`出现错误，但是`except`中的异常名称都没有匹配上，则所有的`except`语句将会被提交到上一级的`try`语句，或者程序的最上层。
   >
   >    如果`语句0`没有错误，则执行`else`下的`语句e`
   >
   >    Tips：异常名称就是错误码，`else`语句不是必须存在的，可以不写

   ```python
   # 不匹配异常名称，只要存在异常就执行语句2
   try:
       语句1
   except:
       语句2

   # 用一个except匹配多个异常，统一处理执行语句2
   try:
       语句1
   except(Except_name_1, ......, Except_name_N):
       语句2

   # finaly语句
   try:
       语句0
   except 异常名称1 as variable:
       语句1
   except 异常名称2 as variable:
       语句2
   ......
   except 异常名称n as variable:
       语句n
   finally:
       语句f
   ```

   > 作用:`语句0`无论是否产生异常都会执行最后的`语句f`，常用于文件操作

3. 断言:

   > 1. 定义:判断一个表达式的值，为真则继续执行程序，为假则抛出一个自定义信息的AssertionError异常
   > 2. 格式:`assert(expression)，"异常信息"`

   ```python
   def func1(num1, num2):
       assert(num2 != 0),"num2不能为0"
       return num1 / num2
   func1(5, 0)
   # 此时会抛出一个信息为"num2不能为0"的AssertionError异常
   ```

4. 特殊:

   > 1. 异常其实是class(类),所有的异常都继承自`BaseException`(这是所有异常的基类)，如果当匹配的异常名称中存在`BaseExcept`这个异常名时，它将匹配所有的异常，包括它的子类，在`BaseExcept`语句后的语句都不会再匹配
   > 2. 跨越多层调用。如果检测的语句中包含多重调用，只要它调用中的存在异常，都可以进行捕获并处理

   ```python
   # 示例1
   # 当语句1产生异常时，如果匹配到ZeroDivisionError则会打印第一个err，因为它在BaseExcept语句之前，但即使语句1出现SyntaxError,它只会匹配到第二个except语句，因为BaseExcept时所有异常的基类，它会捕获所有的异常类型
   try:
      语句1
   except ZeroDivisionError as err:
      print(err)
   except BaseExcept as err:
      print(err)
   except SyntaxError as err:
      print(err)
   ```

   ```python
   示例2
   # 当语句1产生异常时，会在except语句的列表中进行匹配，如果匹配到对应的异常名称则执行语句2
   try:
       语句1
   except(ZeroDivisionError,SyntaxError):
       语句2
   ```

## 文件的读写

1. 打开和关闭文件:

   > 打开文件：`open(path, "flag"[, encoding][, errors])`
   > path：要打开文件的路径
   >
   > flag：文件打开的方式
   >
   > encoding：编码方式
   >
   > errors：错误处理
   >
   > 关闭文件：`close()`
   >
   > Tips：文件打开后，执行相应的操作。当执行完操作后必须关闭文件。

   | flag | 方式                       | 注意                                     |
   | :--- | :------------------------- | :--------------------------------------- |
   | r    | 只读                       | 文件描述符(光标)在文件的开头             |
   | rb   | 以二进制格式打开，用于只读 | 文件描述符(光标)在文件的开头             |
   | r+   | 读写                       | 文件描述符(光标)在文件的开头             |
   | w    | 只写                       | 如果文件存在，则覆盖。否则，新建一个文件 |
   | wb   | 以二进制的方式写入，只写   | 如果文件存在，则覆盖。否则，新建一个文件 |
   | w+   | 读写                       | 如果文件存在，则覆盖。否则，新建一个文件 |
   | a    | 追加写入                   | 如果文件存在，文件描述符在文件的末尾     |
   | a+   | 读写                       | 如果文件存在，文件描述符在文件的末尾     |

2. 读取文件

   > 1. 读取全部文件：`read()`
   >
   > 2. 读取指定字符数：`read(num)`和`readline(num)`
   >
   > 3. 读取整行，包含`\n`字符：`readline()`
   >
   > 4. 读取所有行，并返回一个列表：`readlines()`
   >
   >    Tips:如果给`readlines(num)`传入num,且num大于0。则返回实际size字节的行数。
   >
   > 5. 修改描述符位置：`seek(num)`
   >
   >    当文件进行过读取操作后，读取到什么位置，则文件的描述符移动到相应的位置。如果要读取指定位置的数据则需要将文件描述符移动到指定的位置。num指定了文件描述符移动到第几个字符的后面，从文件的开始算起

   ```python
   # 一个完整的过程
   # 示例
   try:
       path = r"F:\Code\Python\1.txt"
       f1 = open(path, "r")
       print(f1.read())
   finally:
       if f1:
           fi.close()

   # 简单写法
   path = r"F:\Code\Python\1.txt"
   with open(path, "r",encoding = "utf-8") as f1:
       print(f1.read())
   # with语句会在运行完后自动关闭文件
   ```

3. 写入文件：`write()`

   > 1. 写入的数据会存入缓冲区，而不是立刻写入到文件中，当文件关闭时才会将缓冲区中的数据写入到文件中。
   > 2. 使用`flush()`刷新缓冲区，可以让数据立刻写入到文件中
   > 3. 当缓冲区满了，缓冲区中的文件也会被写入到文件中

4. string的编码与解码

   > 当写入时，打开文件指定的什么`encoding`，那么读取时，打开文件必须使用一样的`encoding`
   > 如果打开文件是指定的是以二进制方式写入或读取，那么在写入时必须对string进行编码，读取时必须对string进行解码

5. 要对list、tuple、dict、set这些类型的数据进行文件操作，须使用`pickle`模块

## 面向对象

类：对一类事物的统称

对象：对某一事物的具体描述

结构：

```python
#定义
class ClassName:
    # 类变量（变量--静态字段--静态属性）
    # 类方法（函数--动态字段--动态属性）
    class_suite #类体
#使用
#实例化对象。用 . 跟变量名或方法名进行调用，方法中可以传参
p = ClassName()

```

特点：

1. 类都有一个`__dict__`属性，因为默认的类中的数据都是以字典形式表现的，变量名对应变量的值，方法对应函数在内存中的地址。

2. 在类中定义类方法时，默认会有一个 self 的形参，self 是实例化后的对象名

3. 使用对象调用类方法时，默认会将对象名隐形传入调用的类方法中，但直接使用类名调用类方法时，不会将类名隐形传参

4. 实例化对象后，对象的空间和原始类名指向的不是同一片空间，所以对对象空间中的变量或方法进行操作时不会，改变原类空间中的方法和变量

5. 依赖关系：将一个对象当作参数传递到类中使用就是依赖关系

   ```python
   class ClsName:
       def __init__(self,name,age):
           self.name = name
           self.age = age

       def see(self,other):
           ptint(self.name+"看了"+other.name)

   p = ClsName('leon',12)
   p1 = ClsName('lili',14)
   p.see(p1)

   ```

### 魔法方法

也称为初始化函数，是类在实例化对象时，利用不同对象的传参，初始化类中的变量。是一个给对象空间封装属性的函数

```python
class NewClass:
    def __init__(self,a,b):
        #给对象空间封装属性的函数
        self.name = a
        self.age = b

p = NewClass('leon',12)
print(p.name,p.age)
```

### 类成员

私有成员：

1. 私有变量：
   1. 成员的私有变量：在魔法方法中的所有变量都是私有变量，每个变量的值只能由实例化后的对象访问。在类内部要访问，成员的私有变量只能使用`self.变量名`进行访问。在外部无法使用类名直接访问成员的私有变量
   2. 私有类变量：在类中用双下划线`__变量名`命名的变量为，类的私有变量。类的私有变量无法被实例化后的对象访问，也无法通过类名直接访问，只能在类的内部使用
2. 私有方法：在类的内部使用双下划线`__funName`定义的方法，是私有类方法。实例化后的对象无法访问私有类方法，也无法使用类名直接访问私有类方法。在类的内部可以用`self.__funName()`调用（也可以用ClassName.__funName()进行调用但需要传参），类内部的共有方法也可以直接调用私有类方法

共有成员：类中定义的其他变量或方法都是共有成员，每个实例化后的对象都可以直接访问
