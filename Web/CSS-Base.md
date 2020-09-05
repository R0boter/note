
## 简介

CSS 全称 Cascading Style Sheets 层叠样式表，用于设置网页中的文字（大小、颜色、字体风格、对齐方式等）、图片和排版等

## 基础语法

```html
/* 构建 CSS 运行环境，CSS 包裹在 style 标签中可以在网页中任何位置 一般放在 head 标签内 */
<style>
/* 选择对应元素。可以是标签名也可以是元素 ID 属性的值，也可以是 class 属性的值 */
    div{
            /* 定义内容由 属性:值; 这样的键值对构成 */
        width:200px;
        height:200px;
        background:#FF0000;
        transition:all 2s ease;
    }
/* 注释 */
</style>
```

**Tips：**当使用外联样式时，存在CSS文件中的修饰不用添加`<style>`标签

## 样式分类

1. 内联样式：直接写在 HTML 文件中的 `<style></style>` 标签中

2. 行内样式：直接写在标签的`style`属性中

3. 外联样式：引入外部的CSS文件

   ```HTML
   <!DOCTYPE HTML>
   <HTML>
       <head>
           <meta charset="utf-8">
           <title>标题</title>
           <!-- 外联样式：正式使用首推 -->
           <link rel="stylesheet" type="text/css" href="path">
           <!-- 外联还可以使用指令关联 -->
           @import url("path")
           <!-- 内联样式：不推荐使用 -->
           <style>
               .box{
                   background:red;
               }
           </style>
       </head>
       <body>
           <div class="box">
               这是一个盒子
           </div>
           <!-- 行内样式：后期修改时使用 -->
           <div style="width:100px;height:100px;background:#FF0000;">
               这是行内样式
           </div>
       </body>
   </HTML>
   ```

## 样式的继承和覆盖

### 继承

1. 可继承的CSS属性有：font 系列、text 系列、color、line-height
2. div 可以继承父标签的宽度，但不能继承高度

### 覆盖

当父元素和子元素设置了同样的属性，子元素设置的属性生效

## 样式优先级

### 类型的优先级

行内样式 > 内联样式/外联样式

**Tips：内联样式和外联样式不存在优先级问题，谁后渲染谁生效**。

### 强制优先

在属性值后加`!important` 强制使用此属性值渲染。强制优先级只能用于单个属性

```CSS
background:#00FF00 !important;
```

### 选择器优先级

**伪类选择器首字母 > 伪类选择器首行 > !important > id选择器 > 类名选择器/属性选择器 > 标签名选择器 > 通配选择器**。

**Tips：容易被覆盖的应该写在前面，方便优先级高的覆盖它**。

### 样式叠加（权重）

**!important(无穷大)、行内样式(1000)、id(100)、class(10)、标签名(1)**。

## 布局方式

1. 标准流：按照标签默认的特性摆放盒子
2. 浮动流：利用浮动摆放盒子
3. 定位流：利用定位摆放盒子

## 基础选择器

```html
<!DOCTYPE HTML>
<HTML>
    <head>
        <meta charset="utf-8">
        <title>标题</title>
    </head>
    <body>
        <h1>标题</h1>
        <div id="myid">盒子</div>
        <p class="p1">段落</p>
    </body>
    <style>
        /* 标签选择器：通过标签来选择元素 */
        h1{
            font-family:"微软雅黑";
        }
        /* id 选择器：通过 id 来选择元素 */
        #myid{
            color:#FF0000;
        }
        /* 类选择器：通过 class 来选择元素 */
        .p1{
            font-size:bold;
        }
    </style>
</HTML>
```

## 关系选择器

```HTML
<!DOCTYPE HTML>
<HTML>
    <head>
        <meta charset="utf-8">
        <title>标题</title>
    </head>
    <body>
        <div>
            <p>
                DIV里面的段落
            </p>
        </div>
        <div>第一个是盒子</div>
        <p>第二个是段落</p>
        <p>第三个也是是段落</p>
    </body>
    <style>
        /* 后代选择器（利用祖宗选择指定标签），会迭代选择，两个标签名中间有空格
           祖宗元素和子孙元素不限制是标签名|id名|class名
        */
        div p{
            colo:red;
        }
        /* 子元素选择器，不会迭代选择。父元素和子元素不限制是标签名|id名|class名 */
        div>p{
            font-style:normal;
        }
        /* 兄弟选择器，哥哥标签+弟弟标签，修饰的是弟弟标签。不能通过弟弟选择哥哥 */
        div+p{
            font-size:50px;
            color:red;
        }
    </style>
</HTML>
```

## 复合选择器

```html
<!DOCTYPE HTML>
<HTML>
    <head>
        <meta charset="utf-8">
        <title>标题</title>
    </head>
    <body>
        <!-- 一个标签多个class名 -->
        <div class="ft30 red">这是一个盒子</div>
        <span class="ft30">这是文本</span>
        <p class="ft30">段落部分</p>
        <a href="#" class="ft30">超链接</a>
        <b class="red">文字加粗</b>
        <div class="ft30">另一个盒子</div>
    </body>
    <style>
        .ft30{
            font-size:30px;
        }
        .red{
            color:red;
        }
        p{
            color:green;
        }
        /* 使用多个类名选择同一个元素 */
        .ft30.red{
            text-decoration:underline;
        }
        /* 使用标签加类名选择同一个元素，标签名和类名之间没有空格 */
        div.ft30.red{
            font-width:bold;
        }
        /* 多元素选择器，每个元素用逗号隔开 */
        div,p,span{
            color:green;
        }
    </style>
</HTML>
```

## 通配选择器

```CSS
<style>
    *{
        /* 对网页中所有标签都生效，通常用于设置 padding 和 margin 属性 */
        padding:0;
        margin:0;
    }
</style>
```

## 伪类选择器

语法：

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
        <title>标题</title>
    </head>
    <style>
        /*
        1. link 和 visited 只对 a 标签有效
        2. active 和 hover 对所有元素有效
        */
        /* 正常链接 */
        a:link{color:red;}
        /* 链接点击以后 */
        a:visited{color:green;}
        /* 鼠标点击时 */
        a:active{color:yellow;}
        /* 鼠标移动到目标时 */
        a:hover{font-size:30px;}
    </style>
    <body>
        <a herf="#">百度</a>
    </body>
</html>
```

示例：

```HTML
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
        <title>标题</title>
        <style>
            .box{
                width:200px;
                height:200px;
                background:#abcdef;
                }
            /* 当鼠标放到 .box 上时，对 .box1 进行修饰 */
            .box:hover .box1{
                width:300px;
                height:300px;
                background:#FF0000;
                }
        </style>
    </head>
    <body>
        <div class="box">
            <div class="box1"></div>
        </div>
    </body>
</html>
```

## 伪对象选择器

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
        <title>标题</title>
        <style>
            /* 选择第一行 */
            div:first-line{
                color:green;
            }
            /* 选择第一个字 */
            p:first-letter{
                font-size:20px;
                color:red;
            }
        </style>
    </head>
    <body>
        <div>
            他还说，包括印度在内的一些国家认识到新冠病毒疫情的严重性，已及时开展全面的抗击行动。莫迪还称赞印度民众在封锁期间的表现，“成熟的、前所未有的”
        </div>
        <h1>我爱学习</h1>
        <p>我爱杯中酒</p>
        <p>爱之不可得</p>
        <p>学道北海仙</p>
        <p>习其势翩翩</p>
    </body>
</html>
```

## 属性选择器

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
        <title>标题</title>
        <style>
            /* 一般主要使用属性名和属性名=属性值 */
            /* 属性名 */
            [age]{
                color:red;
            }
            /* 属性名=属性值 */
            [age="12"]{
                width:200px;
            }
            /* 当属性有多个值时，只要有一个值匹配就进行修饰 */
            [name~="asd"]{
                color:#FF0000;
            }
            /* 当属性中有连字符（-）时，指定连字符前的第一个单词 */
            [name|="username"]{
                height:100px;
            }
            /* 当属性的值中存在指定的字符时，就进行修饰 */
            [name*="d"]{
                width:50px;
            }
        </style>
    </head>
    <body>
        <input type="text" name="username-uuu aaa" age="12">
        <input type="password" name="password-uuu asd">
        <input type="submit">
    </body>
</html>
```
