

## Pickle模块

1. 作用:对list、tuple、dict、set类型的数据进行文件操作

2. 写入文件:`pickle.dump(data_name, file_name)`

3. 读取文件:`pickle.load(file_name)`

   ```python
   import pickle
   path = r"F:\Code\Python\1.txt"
   whit open(path, "wb") as f1:
       list1 = [1, 2, 3,"Leon"]
       pickle.dump(list1, f1)
   with open(path, "rb") as f2:
       list2 = pickle.load(f2)
       print(list2)
   ```

## os操作系统

作用:os模块包含了普遍的操作系统的功能

```python
import os
os.name            # 获取操作系统类型，NT -> windows  posix -> linux、unix、Mac OS
os.uname()        # 打印操作系统的详细信息，windows不能使用
os.environ        # 获取操作系统中所有的环境变量
os.environ.get("环境变量名")    # 获取指定的环境变量
os.curdir        # 获取当前路径，即`.`
os.getcwd()        # 获取当前工作目录的绝对路径，即python脚本所在的目录
os.system("shell_command")    # 执行shell命令

# 以下方法都可以指定路径，默认是当前路径下
os.listdir("path")            # 以列表的形式，返回目录下的所有文件
os.mkdir("directory_name")    # 创建目录
os.rmdir("directory_name")    # 删除目录
os.stat("directory_name")    # 获取文件属性
os.rename("old_name", "new_name")    # 重命名
os.remove("file_name")        # 删除普通文件

# 有些方法存在os里，还有些存在于os.path里
os.path.abspath("path")        # 获取指定的绝对路径，通过相对路径指定path
os.path.join("path1","path2")# 拼接路径，path2的开始处不能存在斜杠
os.path.split("path")        # 拆分路径，返回一个tuple，第二个元素为路径最后的文件
os.path.splitext("path")    # 获取扩展名，返回一个tuple，第二个元素为路径最后的文件的扩展名，如果最后还是一个目录，那么tuple的第二个元素为空
os.path.isdir("path")        # 判断指定的路径是否是目录，是返回Ture,不是返回False
os.path.isfile("path")        # 判断文件是否存在，是返回Ture,不是返回False
os.path.exists("path")        # 判断目录或文件是否存在，是返回Ture,不是返回False
os.path.getsize("path")        # 获取文件大小，以字节为单位
os.path.dirname("path")        # 获取指定文件的路径
os.path.basename("path")    # 获取指定文件的文件名
```

## Turtle绘图

1. 运动方法:

   ```python
   import turtle
   turtle.forward(x)        # 向前移动x长度
   turtle.backward(x)        # 向后移动x长度
   turtle.right(x)            # 向右旋转x度
   turtle.left(x)            # 向左旋转x度
   turtle.goto(x,y)        # 移动到坐标为x,y的位置
   turtle.speed(x)            # 笔画绘制的速度，x取值范围在0-10之间
   ```

2. 笔画控制方法:

   ```python
   turtle.up()                # 笔画抬起，移动不会绘制线条
   turtle.down()            # 笔画落下
   turtle.setheading(x)    # 改变朝向
   turtle.pensize(x)        # 设置笔画宽度
   turtle.pencolor("color")# 设置笔画颜色，color为英文单词
   turtle.reset()            # 清空窗口，并重置画笔设置
   turtle.clear            # 清空窗口，但不会重置画笔
   turtle.circle(x, steps=y)# 绘制一个y边形，x为半径，steps不设置，则画圆

   turtle.begin_fill()        # 开始填充
   turtle.fillcolor("color")# 填充的颜色
   turtle.end_fill()        # 结束填充
   ```

3. 其他方法:

   ```python
   import turtle
   turtle.done()            # 保持程序继续执行
   turtle.undo()            # 撤销上一次操作
   turtle.hideturtle()        # 隐藏海龟
   turtle.showturtle()        # 显示海龟
   turtle.screensize(x, y)    # 设置画板大小
   ```

4. Tips:海龟绘图是一个简单的绘图工具，绘图窗口的原点(0, 0)在窗口正中间，默认方向朝右
