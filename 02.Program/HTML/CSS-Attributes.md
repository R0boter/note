# CSS 属性

## 字体属性

像素（Pixel）是指构成图片的小色点，分辨率（单位：DPI）是指每英寸（lnch）上的像素数量，可以看作是像素的分布密度；像素相同时，分辨率越高则像素密度越大，图像越清晰

```CSS
/* html 中默认字体 16px 大小 */
div{
    /* 设置文字大小*/
    font-size:30px;
    /* 设置字体粗细,加粗的值为 bold */
    font-weight:bold;
    /* 设置字体风格,取值normal一般用于将倾斜字体不倾斜，常用于 i 标签，italic 是将正常字体设置倾斜 */
    font-style:normal;
    /* 设置字体,字体可以设置多个用逗号隔开 */
    font-family:"宋体";
    /* webdings 字体是由数字或字母表示 */

    /* 宽 */
    width:300px;
    /* 高 */
    height:300px;
}
```

## 文本修饰

```CSS
a{
    /* none:取消下划线，line-through：贯穿线（删除线），overline：上划线，underline：下划线。一般会把超链接的下划线取消 */
    text-decoration:none;
}
p{
    /* uppercase:将所有字母转换为大写，lowercase：将所有字母转换为小写，capitalize：将所有单词首字母大写 */
    text-transform:uppercase;
    /* 文本对齐方式：left|right|center */
    text-align:left;
    /* 首行缩进：也可以使用固定像素为单位会导致字体大小更改时，缩进更改，所以使用字符为单位 em */
    text-indent:2em;
}
```

## 颜色

```CSS
p{
    /* 文字颜色，和HTML颜色定义一样 */
    color:#000000;
    /* 文字背景颜色 */
    background:#000000;
}
```

## 行高属性

```CSS
div{
    /* 设置每一行的高度，常用于让文字在盒子中垂直居中 */
    line-height:30px;
}
```

## 背景属性

```CSS
div{
    /* 设置背景颜色，设置背景透明时只能使用rgba()的方式，透明取值0-1 */
    background-color:#eee;
    /* 设置背景图片，图片默认是平铺的（如果图片尺寸大于标签会延申出去，如果图片尺寸小于标签则会复制自身) */
    background-image:url(path);
    /* 设置背景图片平铺效果：
    repeat 允许图像平铺
    no-repeat 不允许平铺，
    repeat-x 允许图片横向平铺，
    repeat-y  允许图片纵向平铺 */
    background-repeat:no-repeat;
    /* 设置背景图片大小 第一个值是宽度，第二个值是高度 */
    background-size:200px 200px;
    /* 调整背景图的位置
    使用像素值定位：数值第一个值代表水平距离（左上角），第二个值代表垂直距离
    使用关键字定位：top|bottom|left|right|center
    使用百分比定位：以图片中心点到标签左上，第一个值表示水平距离，第二个值表示垂直距离
    */
    background-position:20px 4px;
    background-position:top center;
    background-position:50% 50%;
    /* 综合写法：颜色 图片 是否平铺 定位/大小（定位和大小的顺序不能调换） */
    background:#eee url(path) no-repeat top center/200px 200px;

    /* 设置背景图不受滚动条影响（固定）：fixed*/
    background-attachment:fixed;

    /* 设置背景颜色渐变 */
    /* 线性渐变，默认方向是从上到下，默认颜色停止点是 50%
    background:linear-gradient([to 方向],color [color-stop],...)
    方向除了用【to 方向】还可以直接使用度数表示如【45deg】表示45度角方向为左下角到右上角【135deg】表示135度角，方向为左上角到右下角
    */
    background:linear-gradient(to right,red 20%,green 50%);
    /* 径向渐变
    background:radial-gradient([ellipse|circle 100px at right bottom],color [color-stop],...)
    设置形状：ellipsel表示椭圆，circle表示圆形（默认），后面跟像素大小可以指定渐变范围，椭圆需指定长宽。还可以使用at设置圆心位置，默认center在中心
    设置颜色和颜色停止点：
    */
    background:radial-gradient(red %20,yellow 70%);
}
```

## 列表属性

```CSS
ul{
    /* 取消列表前的符号 */
    list-style-type:none;
    /* 使用自定义图片做列表符号 */
    list-style-image:url(path);
    /* 通用方法:一般使用通用方法去掉列表前符号，搭配padding和margin去掉边缘间距 */
    list-style:none;
    padding:0;
    margin:0;
}
```

## 内容溢出处理

```CSS
div{
    /*
    内容溢出处理：
    auto：自动生成滚动条，
    hidden：超出部分隐藏，
    scroll：右边和下边都有滚动条
    只设置水平方向溢出处理用overflow-x
    只设置垂直方向溢出处理用overflow-y
    */
    overflow:hidden;
}
```

## 标签显示模式的属性

```CSS
div{
    /*
    使用display可以将标签的显示模式进行转换
    block：转为块元素
    inline：转为行元素
    inline-block：转为行内块元素
    none：隐藏模式
    */
    display:inline-block;
}
```

## 盒子模型（标准流布局）

```CSS
div{
    /*
    内间距（内填充）：当设置了内填充后应当在对应的宽度或高度上减去填充的距离,CSS3中新增内减模式自动去除影响，不用手动减去填充距离
    padding[-top|left|right|bottom]:10px;
    当只使用padding时：
    一个值：代表上下左右都填充同等的像素大小
    两个值：第一个值代表上下，第二个值代表左右
    三个值：第一个值代表上，第二个值代表左右，第三个值代表下
    四个值：第一个值代表上，第二个值代表右，第三个值代表下，第四个值代表左
    */
    padding:0px;

    /*
    外间距
    margin[-top|left|right|bottom]:10px;
    当只使用margin时：
    一个值：代表上下左右都填充同等的像素大小
    两个值：第一个值代表上下，第二个值代表左右
    三个值：第一个值代表上，第二个值代表左右，第三个值代表下
    四个值：第一个值代表上，第二个值代表右，第三个值代表下，第四个值代表左
    */
    margin:10px;
    /* 使块元素在父元素中居中 */
    margin:0 auto;
    /* 常用清除间距 */
    padding:0px;
    margin:0px;
}
```

### 边框

```CSS
div{
    /* 边框类型
    none：去除边框
    hidden：和none相同，但当用于表时，是用于解决边框冲突问题
    dotted：点状边框
    dashed：虚线边框
    solid：实线边框
    double：双线边框，双线的宽度等于border-width的值
    groove：3D凹槽边框，效果取决于border-color的值
    ridge：3D垄状边框，效果取决于border-color的值
    inset：3D凹陷边框，效果取决于border-color的值
    outset：3D凸出边框，效果取决于border-color的值
    inherit：规定从父元素继承边框样式
    */
    border-style:none;

    /* 边框颜色：
    默认值为transparent，表示边框颜色为透明
    inherit：规定从父元素继承边框颜色
    */
    border-color:#FFFFFF;
    /* 边框宽度 */
    border-width:20px;
    /* 简便写法，每个值用空格隔开 */
    border:double #0000FF 10px;

    /* 设置单个方向的边框：border[-top|left|right|bottom]
    1. 边框会占据位置，大小为border-width的值
    2. 利用边框可以自定义出多种图形
    */
    /* 三角形 */
    width:0px;
    height:0px;
    border-top: 40px solid transparent;
    border-right: 40px solid transparent;
    border-left: 40px solid yellow;
    border-bottom: 40px solid transparent;

}
```

### 圆角

```CSS
div{
    width:100px;
    height:100px;
    background:#FF0000;
    /*  */
    border-radius:20px;
}
```

## 元素隐藏

```CSS
.box1{
    width:400px;
    height:400px;
    background:#FF0000;
}
.box2{
    width:100px;
    height:100px;
    background:#00FF00;
    /* 让元素隐藏，不占用空间 */
    display:none;
    /* 让元素隐藏，会占用空间 */
    visibility:hidden;
}
.box1:hover .box2{
    /* 让隐藏的元素以块元素的方式显示 */
    display:block;
    /* 让隐藏的元素显示 */
    visibility:visible;
}
```

## 伪对象

```css
div{
    width:400px;
    height:400px;
    background:#00FF00;
}
div::before{
    /* 伪对象：在指定元素的内部的前面添加 */
    content:"开头";
    display:block;
    background:#FF0000;
    font-weigh:bold;
    text-align:center;
}
div::after{
    /* 伪对象：在指定的元素的内部的后面 */
    content:"结尾";

/*
注意：
    1. 伪对象不是一个实际标签，是css样式模拟的一个标签
    2. 伪元素必须有 content 属性
    3. 伪元素是行元素
    4. 官方推荐使用双冒号，但实际使用中推荐单冒号
*/
}
```

## 浮动布局

```css
/* 当元素被设置为浮动时：
1. 块元素不再独占一行
2. 浮动的元素可以重叠在没有浮动的元素上面，但不会覆盖文字
3. 要想让多个块元素在同一行显示，必须给所有块元素都加上浮动
4. 浮动的最大价值在于让元素排列成一行，或者一左一右
5. 浮动后的元素，都变为行内块
6. 浮动的元素脱离了标准流
*/
.box1{
    width:100px;
    height:100px;
    background:#FF0000;
    /* 向左浮动 */
    folat:left;
}
.box2{
    width:200px;
    height:200px;
    background:#00FF00;
    /* 向右浮动 */
    folat:right;
}
.box3{
    width:300px;
    height:300px;
    background:#0000FF;
    /* 取消浮动 */
    folat:none;

    /*
    1. 浮动最开始用于图文绕排
    2. 现在最多用于将多个块元素排成一行
    3. 加了浮动后元素的顺序，以标签编写顺序，而且要朝同一方向
    */
}
```

### 浮动带来的问题

当元素浮动后，因为浮动元素脱离了标准流,，不再占用标准流空间，所以浮动元素无法再撑开父元素，父元素原本的位置会被父元素的兄弟元素占用

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1{
            width: 500px;
            background: #742424;
        }
        .box1 div{
            width: 100px;
            height: 100px;
            float: left;
        }
        .s1{
            background: #a7d433;
        }
        .s2{
            background: #adadad;
        }
        .s3{
            background: #ff00ff;
        }
        .box2{
            width: 500px;
            height: 200px;
            background: #a5a3acdd;
        }
    </style>
</head>
<body>
    <div class="box1">
        <div class="s1"></div>
        <div class="s2"></div>
        <div class="s3"></div>
    </div>
    <div class="box2"></div>
</body>
</html>
```

### 消除浮动的问题

1. 给父元素设置固定高度（不推荐使用，因为实际开发中很多盒子不是固定高度）

2. 在父元素后设定空标签清除浮动

   ```css
   .clear{
       /* 必须先在网页中要清除浮动的元素的下面添加一个空的块元素，专门用于清除浮动 */
       clear:both;
   }
   ```

3. 设定父元素的`overflow`

4. 利用伪对象添加空标签来清除浮动

   ```css
   div::after{
       content:"";
       height:0px;
       clear:both;
       overflow:hidden;
       display:block;
   }
   ```

## 阴影

   ```css
   div{
       width:100px;
       height:100px;
       /* 文本阴影：text-shadow:横向偏移 纵向偏移 模糊距离 颜色,...;
       一个文字可以有多个阴影，用逗号隔开
       */
       text-shadow:5px -5px 2px #999;

       /* 盒子阴影：box-shadow:水平偏移 垂直偏移 模糊距离 阴影尺寸 颜色 */
       box-shadow:8px -3px 10px 10px #F00;
   }
   ```

## 细线表格

表格间的边框实际上是重叠在一起的，使用细线表格可以优化表格间的边框

```css
table{
    /* 细线表格 */
    border-collapse:collapse;
}
```

## 定位布局

定位的方式：静态定位、相对定位、绝对定位、固定定位

定位的偏移属性：left、right、top、bottom

**Tips：**偏移值表示距离什么位置有多少像素

### 静态定位

所有的标准流都是静态定位，设置静态定位和不设置没有区别。偏移值对静态定位无效，通常用于将设置过定位的元素还原成标准流

语法：`position:static;`

### 相对定位

语法：`position:relative`

```css
div{
    width:200px;
    height:200px;
    background:#00FF00;
    /* 设置相对定位 */
    position:relative;
    top:50px;
    left:100px;
    /*
    1. 参考自身在标准流中的位置进行偏移
    2. 可以覆盖别的元素
    3. 偏移后，原本的位置还是占用空间
    4. 常用于对元素位置的微调
    */
}
```

### 绝对定位

语法：`position:absolute;`

```css
.box{
    width:200px;
    height:200px;
    background:#FF0000;
    /* 设置绝对定位 */
    position:absolute;
    top:50px;
    left:100px;
    /*
    1. 偏移位置参考设置过定位（相对|绝对|固定）的直系父元素或直系祖宗元素，没找到就一直往上找，直到 html
    2. 绝对定位脱离了标准流，不继承父级宽度（无论是块元素还是行元素，盒子大小取决于其中的内容），可以自定义宽高，不占用标准流空间，会覆盖文字
    3. margin:auto; 对设置过绝对定位的元素不起作用
    4. 设置方向偏移时，横向或纵向只设置一个即可，设置多个没有意义
    5. 使用场景多用于配合相对定位使用
    */
}
```

### 固定定位

语法：`pasition:fixed;`

```css
.box{
    width:3000px;
    height:200px;
    background:#abcdef;
    /* 设置固定定位：相对于浏览器窗口 */
    pasidion:fixed;
    /* 让盒子在父元素中居中 */
    left:50%;
    top:50%;
    margin-left:-150px;
    margin-top:-100px;

    /*
    1. 固定定位时以浏览器作为参考进行偏移的，且滚动条对固定定位无效
    2. 会脱离标准流，不占据标准流空间
    3. margin:auto; 对固定定位无效
    4. 不会随滚动条滚动，永远固定在浏览器窗口中的固定位置
    5. 常用于网页右下角的回到顶部和网页两侧的广告
    */
}
```

### 定位元素的层级效果

用于控制当多个定位后的元素叠放在同一位置时的层级效果

语法：`z-index:num`

取值：

1. 正数：数字越大，层级越高，离用户越近
2. 负数：数字越小，层级越低，离用户越远
3. `auto`：默认值，和父级元素层级相同，按照渲染顺序进行层叠
4. 正数比 auto 大，负数比 auto 小

## CSS3 和 CSS2 区别

### 内减模式

用于将 `padding` 内填充和边框带来的增大盒子的影响消除掉

语法：`box-sizing:border-box;`

```css
.box{
    width:200px;
    height:200px;
    background:#FF0000;
    padding:50px;
    border: 40px solid yellow;
    /* 内减模式，消除padding和边框问题 */
    box-sizing:border-box;
}
```

### 新增的属性选择器

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8">
        <title>页面的标题</title>
        <style>
            /* 指定以a开头的属性名的标签 */
            [name^="a"]{
                color:red;
            }
            /* 指定以u结尾的属性名的标签 */
            [name$="u"]{
                color:blue;
            }
        </style>
    </head>
    <body>
        <input type="text" name="name kj ufknu">
        <input type="text" name="user">
        <input type="text" name="adsfiu">
        <input type="text" name="adb">
    </body>
</html>
```

### 新增伪类选择器

重点在 `li:first-child`、`li:last-child`、`li:nth-child(n)`、`li:nth:-child(2n+1)`奇数元素

其他基本不用（新增的伪类选择器还存在兼容性问题）

|     伪类选择器     |                 作用                 |
| :----------------: | :----------------------------------: |
|      `:root`       |                根标签                |
|   `:first-child`   |    代表找出父元素中的第一个子元素    |
|   `:last-child`    |   代表找出父元素中的最后一个子元素   |
|  `:nth-child(n)`   |     找出父元素中的第 n 个子元素      |
| `:nth-child(even)` |       找出父元素中奇数的子元素       |
| `:nth-child(odd)`  |     代表找出父元素中偶数的子元素     |
|      `:empty`      | 代表找出父元素中子元素内容为空的标签 |
| `:nth-of-type(n)`  |        找出指定标签中的第n个         |
|  `:first-of-type`  |        找出指定标签中的第一个        |
|  `:last-of-type`   |       找出指定标签中的最后一个       |
|   `:only-child`    |  找出指定标签是父标签中的唯一子元素  |

## 2D 变换效果

可以设置移动、旋转、大小

```css
.box{
    width:500px;
    height:500px;
    background:red;
}
.s1{
    width:100px;
    height:100px;
    background:blue;
}
.box:hover .s1{
    /* 当鼠标移动到.box上时，.s1横向移动200px，垂直移动100px */
    transform:translate(200px,100px);

    /* 当鼠标移动到.box上时，.s1顺时针旋转135度 */
    tranfrom:rotate(135deg);

    /* 当鼠标移动到.box上时，.s1放大2倍。放大使用正整数，缩小使用小数 */
    transfrom:scale(2);
    /* 当鼠标移动到.box上时，.s1宽度放大2倍，高度放大3倍 */
    transfrom:scale(2,3);
    /* 三个属性可以写在同一个里面，用空格隔开 */
    transfrom:rotate(360deg) scale(2);

    /* 当鼠标移动到.box上时，.s1绕x轴旋转45度（斜切）
    第一个值表示绕 x 轴旋转，第二个值表示绕 y 轴旋转
    此属性的放大缩小是以中心进行放大缩小
    */
    transfrom:skew(45deg,0);
}
```

## 过渡效果

语法：`transition:transition-property transition-duration transition-timing-function transition-delay`

1. `transition-property`：规定设置过渡效果的 CSS 属性名
   1. `none`：没有属性会获得过渡效果
   2. `all`：所有属性都会获得效果
   3. `property`：定义应用过渡效果的 CSS 属性名称，多个属性名用逗号隔开
2. `transition-duration`：规定完成过渡效果需要多少秒
3. `transition-timing-function`：规定速度效果的速度曲线
   1. `linear`：以相同的速度开始到结束的过渡效果
   2. `ease`：规定慢速开始，然后变快，然后慢速结束的过渡效果
   3. `ease-in`：规定以慢速开始的过渡效果
   4. `ease-out`：规定以慢速结束的过渡效果
   5. `ease-in-out`：规定以慢速开始和结束的过渡效果
   6. `cubic-bezier(n,n,n,n)`：再 cubic-bezier 函数中定义自己的值，范围在 0-1 之间
4. `transition-delay`：定义过渡效果开始前需要等待的时间

```css
img{
    display:block;
    margin 50px auto;
    boder:1px solid #000;
    /* 添加过渡效果，必须在元素原本的样式上添加，不能再伪类上添加 */
    transition:transfrom 2s linear;
}
img:hover{
    transfrom:scale(1.5);
}
```

## 光标形状

语法：`cursor:值`

取值：

1. `text`：文本图标
2. `help`：问号图标
3. `wait`：等待图标
4. `pointer`：小手图标
5. `move`：移动
6. `url(),临时替换的样式`：需要在 url 后面加 auto。所引用图片不能过大，过大无效
7. `default`：箭头

## 盒子轮廓

和边框类似，值也和边框一样，但包裹在边框外面。

一般用`outline:none`来去掉输入框的轮廓，因为当输入框获取光标后，四周的轮廓会变蓝色，此时用去掉边框无效。因为这个蓝色不是边框是轮廓。

## 透明度

语法：`opacity:值`。取值在 0-1 之间，0 是完全透明，元素不可见。1 是完全不透明。

此属性会将该标签中的文字也透明化，使用背景颜色 rgba 模式透明不会导致文字透明

## 文本域的拉伸

语法：`resize:none;`

作用：

1. 取消文本域的拉伸 。多行文本域默认是可以拉伸的，一旦被拉伸容易对页面布局造成影响，使用此属性可以取消文本域的拉伸，防止页面布局被破坏，
   1. 也可以使用此属性设置文本域的默认尺寸大小

## 放大缩小

语法：`zoom:值`。取值正整数为放大，负数为缩小。此属性放大缩小是以左上角进行放大缩小

## 行内文字溢出处理

当行内文字溢出时，使用省略号形式显示

```css
.box{
    width:300px;
    height:100px;
    /* 超出部分隐藏 */
    overflow:hidden;
    /* 设置文本不换行 */
    white-space:nowrap;
    /* 超出文本用省略号代替 */
    text-over-flow:ellipsis;
    /* 必须三条属性都存在，才会生效 */
}
```

## 行内块与文字对齐

语法：`vertical-align:值`。用于控制行内块于文字的对齐方式，写在行内块元素上面

值：

1. `baseline`：图片的基线于文字基线保持对齐
2. `top`：图片的顶线和文字的顶线（行高的顶线）对齐
3. `bottom`：图片的底线和文字的底线（行高的底线）对齐
4. `middle`：图片的中线和文字的中线对齐

四线三格：英文字母的书写由四线三格进行定位，四线分别是顶线、中线、基线、底线。默认使用的是基线对齐，会导致视觉上文字和图片不在同一水平线

## 多栏布局

语法：`column-count:num;`设置分为指定数值栏显示，一般用于文本布局

### 多栏隔断框

语法：`column-rule:5px solid #0f0;`值为边框三要素，其效果和边框类似，在隔断处显示一个宽 5px，颜色为 #0f0 的实线边框

### 设置每一栏的宽度

语法：`column-width:200px;`使用宽度时不使用指定分多少栏，因为此属性就是设置每一栏的宽度，根据宽度会自动设置对应的栏数

## 弹性布局

```css
.box{
    width:300px;
    height:300px;
    border:1px solid #000;
    /* 设置弹性容器
    必须设置此项，表示此元素作为一个弹性容器。弹性容器类似于浮动布局，但并未脱离文档流
    */
    display:flex;
    /* 设置弹性布局的排列方式，此选项在父元素中设置，但是对此元素中的子元素起作用
    row：类似浮动布局的左对齐(默认)
    row-reverse：类似浮动布局的右对齐，但第一位在最右边
    column：垂直排列
    column-reverse：逆向垂直排列
    */
    flex-direction:row;
    /* 设置弹性布局是否换行
    wrap：换行显示
    nowrap：不换行显示（默认）
    wrap-reverse：反转换行显示。会从最下面从左至右排列，填满后换行
    */
    flex-wrap:wrap;
}
.box div{
    width:100px;
    height:100px;
    background:#00F;
    border:2px solid #FFF;
}
```

### 弹性布局的对齐方式

#### 水平对齐

```css
.box{
    width:400px;
    height:400px;
    border: 1px solid #0f0;
    display:flex;
    /*  */
    justify-content:
}
.box div{
    width:100px;
    height:100px;
    background:#00F;
}
```

#### 垂直对齐

```css
.box{
    width:400px;
    height:400px;
    border: 1px solid #0f0;
    /*  */
    align-content:
}
.box div{
    width:100px;
    height:100px;
    background:#00F;
}
```

#### 交叉对齐

```css
.box{
    width:400px;
    height:400px;
    border: 1px solid #0f0;
    /*  */

}
.box div{
    width:100px;
    height:100px;
    background:#00F;
}
```

#### 子元素自己在 Y 轴对齐

```css
.box{
    width:400px;
    height:400px;
    border: 1px solid #0f0;
    /*  */
}
.box div{
    width:100px;
    height:100px;
    background:#00F;
}
```
