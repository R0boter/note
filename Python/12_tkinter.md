
## 创建主窗口

```python
import tkinter

#创建主窗口
root = tkinter.Tk()

#设置主窗口大小，推荐第一中方法
#初始化窗口大小，值是一个字符串，还可以定位窗口再屏幕上的位置
root.geometry('300x300')
#最小窗口大小，值是像素
root.minsize(300,300)


#开启窗口事件循环
root.mainloop()
```

## 创建组件

```python
#lable 标签，显示一段不可编辑的文字

#entry 单行文本框，只能显示单行文本

#text 多行文本框，显示多行文本

#button 按钮，点击时执行一个动作

#checkbutton 复选框，允许用户选择或者反选一个选项

#radiobutton 单选框，运行用户从多个radiobutton中选取一个

#listbox 列表框，一个选项列表，用户可以从中选择

#menu 菜单，点下菜单按钮后弹出一个选项列表，用户可以从中选择

#menubutton 菜单按钮 ，用来包含菜单的组（有下拉式、层叠式等）

#message 消息框，类似于标签可以显示多行文本

#scale 线性滑块，可以设定起始值和结束值，会显示当前位置的精确值

#scrollbar 滚动条，对支持的组件（文本域、画布、列表框、文本框）提供滚动功能

#toplevel 顶层，为其他控件提供单独的容器

#spinbox 输入控件，类似entry，但可以指定输入范围

#panedwindow 窗口布局管理，可以包含一个或多个子控件

#lableframe 容器控件，一个简单的容器控件

#messagebox 消息框，用于显示应用程序的消息框

#canvas 画布，提供绘图功能（直线、椭圆、多边形、矩形）可以包含图形或位图

```

## 组件基本属性

```python
#背景颜色
bg = "colorName|hex color|rgb color"

#前景色
fg = 'colorName|hex color|rgb color'

#字体，以元组形式存在
font = (('黑体', 20, 'bold', 'italic'))

#锚点，以方向的单词首字母定义,定义文字在控件中的位置
anchor = 'sw'

#三维效果，设置控件显示的效果
relief = 'flat'

#位图，设置按钮显示一个预设的位图
bitmap = 'question'

#鼠标样式，当鼠标移动到组件上时，鼠标的显示样式
cursor = 'heart'

#图片，需要先将图片生成为一个图像对象，再引用这个对象
pic = tkinter.PhotoImage(file = 'PicDir')
image = pic


```

## 组件摆放方式

1. `pack()`：只能指定将组件放在界面的上下左右四个位置。默认值是`top`

   ```python
   #设置组件相对于父组件的摆放位置top、down、left、right
   componentName.pack(side = 'left')
   #设置组件内部间距ipadx是内部的左右间距，ipady是内部的上下间距
   componentName.pack(ipadx = 20,ipady = 20)
   #设置多个组件之间的外部间距padx是外部的左右间距，pady是外部的上下间距
   componentName.pack(padx = 20,pady = 20)
   #设置组件占据最大位置fill，x是占据水平方向最大位置只能在side为top或down时使用，y时占据垂直方向最大位置，只能在side为left或right时使用,both是占据整个窗口最大位置，只能在side组件失效时使用
   componentName.pack(side = 'left',fill = 'y')
   componentName.pack(side = 'down',fill = 'x')
   #设置side是否失效expand，yes是失效，默认是no。搭配fill的both选项，让组件占据父组件的最大位置
   componentName.pack(expand = 'yes',fill = 'both')
   ```

2. `grid()`：将界面划分为网格状，按照网格编号进行组件放置。以左上角(0,0)为起始位，适合网格架构

   ```python
   #默认 row 为 0（行数），cloumn 为 0（列数）
   componentName.grid(row = 1,cloumn = 2)
   #rowspan指定跨行，cloumnspan指定跨列，要想组件占满跨行或跨列后的全部空间需要搭配ipadx或ipady一起使用
   componentName.grid(row = 1,cloumn = 2，rowspan = 2, ipadx = 20)
   ```

3. `place()`：安装像素位对组件进行放置，以左上角(0,0)为起始位，适合软件拖放架构

   ```python
   #绝对布局，当
   #设置组件摆放位置，x是设置距离左上角的水平长度，y是设置距离左上角的垂直长度
   componentName.place(x=10,y=20)
   #设置组件的宽度width，高度height
   componentName.place(x=10,y=20,width=10,height=10)

   #相对布局，当主界面大小变化时组件大小随之改变
   #设置组件摆放位置，relx是设置距离左上角的水平长度，rely是设置距离左上角的垂直长度
   componentName.place(relx=0.1,rely=0.2)
   #设置组件的宽度relwidth，高度relheight
   componentName.place(relx=0.1,rely=0.2,relwidth=10,relheight=10)
   ```
