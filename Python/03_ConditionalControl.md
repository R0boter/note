# python 流程控制

## If语句

1. 格式：

   ```python
     if 表达式:
        语句
     elif 表达式:
        语句
     else:
        语句
     # Tips:每一个elif都是对它上面的条件的否定
   ```

2. 逻辑：当程序执行到if语句时，首先计算`表达式`的值，如果为真，则执行语句。为假，则跳过if下所有语句,然后计算elif后`表达式`的值，为真，则执行语句。为假，则跳过elif，如果所有`表达式`的值都为假，则执行else下的语句。

   > 假：0、0.0、''、None、False
   >
   > 真：除了假皆为真

## While语句

1. 格式：

   ```python
     while 表达式:
        语句1
     else:
        语句2
   ```

2. 逻辑：当程序执行到while语句时，首先计算`表达式`的值，如果为真，则执行`语句1`，然后再次计算`表达式`的值，直到结果为假，则执行`语句2`然后跳出循环。`else`不是必须。

## For语句

1. 格式：

   ```python
      for 变量名 in 集合:
         语句
   ```

2. 逻辑：按顺序取`集合`中的`元素`，赋值给`变量名`，然后执行`语句`。如此循环，直到取完`集合`中的所有`元素`

## Break语句

1. 作用：跳出for和while循环
2. 注意：当循环存在嵌套时,`break`只能跳出当前的循环.循环语句存在`else`语句时，如果是`break`语句打断了循环，那么不会执行`else`语句

## Continue语句

1. 作用：跳出当前循环中的剩余语句，然后继续执行下一次循环