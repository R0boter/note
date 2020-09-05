
## 网站图标

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8" />
        <title>标题</title>
        <!-- 设置网站图标 -->
        <link rel="shortcut icon" href="img_path" />
    </head>
</html>
```

## TDK标签SEO优化

```html
<!DOCTYPE HTML>
<html lang="zh-CN">
    <head>
        <meta charset="utf-8"/>
        <!--
网站标题 title
title 具有不可替代性，是内页第一个重要标签，是搜索引擎了解网页的入口和对网页主题归属的最佳判断点
建议：网站名（产品名）-网站介绍（尽量不超过30个字）
-->
        <title>网站名-网站介绍</title>
        <!--
网站说明：description
用于简要说明，网站是做什么的
-->
        <meta name="description" content="网站说明"/>
        <!--
关键字：keywoeds
页面关键字，最好限制再6-8个关键词之间，用英文逗号隔开
-->
        <meta name="keywords" content="关键词1,关键词2"/>
    </head>
</html>
```

## LOGO 的 SEO 优化

1. LOGO 里面放一个 `h1`标签，因为`h1`标签对搜索引擎权重很大
2. `h1`中再放一个链接，可以返回首页，将 LOGO 的背景图片给链接就可以了
3. 为了方便收录，链接里要放文字（网站名称），但文字不要显示出来
   1. 用`text-indent:-9999px;`将文字移到盒子外面，再用`overflow:hidden`。淘宝的方法
   2. 直接给`font-size:0px;`就看不见文字了。京东的方法
4. 最后给链接一个`title`属性，让鼠标放在 LOGO 上可以看到提示文字

## 标题

```html
<h1></h1>
<h2></h2>
<h3></h3>
<h4></h4>
<h5></h5>
<h6></h6>
```

特性：

1. 文字加粗
2. 独占一行
3. h1  最大，h6 最小
4. 有标题的语义，利于 SEO 优化
   1. 竞价排名买关键字、买点击量（及排名靠前时的点击次数）
   2. 规范页面，语义明确，有利于 搜索引擎爬虫的抓取
   3. 发外链，在贴吧、论坛发网站链接

## 段落

```html
<p>
    <!-- 每个段落标记独占一行 -->
</p>
```

## 换行

```html
<br> <!-- 换行标签，单标签，用于嵌套在标题或段落中 -->
<hr> <!-- 画一条水平线，单标签。一般用于标题下面 -->
```

## 字体标记

```html
<b>文字加粗</b>
<i>文字倾斜</i>
<u>文字下划线</u>
<!-- 用于对段落中的文字处理 -->
```

## 强调标记

```html
<strong>加粗强调</strong>
<em>斜体强调</em>
<ins>下划线强调</ins>
<!-- 和字体标记作用一样，在SEO角度，权重更高 -->
```

## 无序列表

```html
<ul type="circle">square
<!--
列表标签需要配合 li 使用
无序列表：每一项不区分顺序
-->
    <li>第一条</li>
    <li>第二条</li>
    <li>第三条</li>
</ul>
```

无序列表有一个 `type`属性可以设置列表项目符号样式

1. `circle`：空心圆
2. `square`：正方形
3. `disc`：实心圆（默认）

## 有序列表

```html
<ol>
<!--
有序列表：ol 配合 li
控制序号类型的属性：Type   a（小写字母）|A（大写字母）|I（罗马数字）|i|1（数字）
控制序号开始的属性：start	 属性值必须是数字，表示从第几个开始
-->
    <li>第一条</li>
    <li>第二条</li>
    <li>第三条</li>
</ol>
```

## 自定义列表

```html
<dl>
<!--
自定义列表：由dl dt dd组成
注意：dt和dd是兄弟结构
-->
    <dt>类似于列表标题的作用</dt>
    <dd>列表内容</dd>
    <dd>列表内容</dd>
    <dd>列表内容</dd>
</dl>
```

## 超链接

```html
<!--
当href的值为单个井号或三个井号时，为一个空白链接
a 标签的target(目标属性)的值：
在框架中定义的 name 的值，在指定的框架中打开新页面
_bkank：跳转到一个新的窗口打开新页面
_self：在原页面的窗口中打开新页面
-->
<a href="https://www.baidu.com" target="_self" title="百度一下">百度</a>
```

### 内部链接

`href`可以使用相对路径，绝对路径可以省略域名，默认从域名根目录开始

### 外部链接

`href`：添加外部链接时必须添加`http://`协议头

### 下载链接

当链接目标无法被浏览器识别时会自动下载链接的目标

### 阻止链接跳转

`href='javascript:;'`或`href='javascript:viod(0);'`点击连接后不会跳转且 URL 中不会显示`#`

## 锚点链接

```html
<!-- top是浏览器关键字 -->
<a href="#top">回到顶部</a>

<!--
锚点链接正规用法，
id为设置锚点，
href的值为井号加设置的锚点值时，点击会直接跳转到锚点的位置
-->
<a id="maodian">这是锚点</a>

<a href="#maodian">直到锚点</a>
<!--
1. 锚点的本质是浏览器页面滚动条的滚动，当没有滚动条时不会进行跳转
2. 当锚点使用 display:none; 隐藏时，因为它不在页面占取空间，所以不会进行跳转
3. 当锚点使用 visibility:hidden; 或 overflow:hidden; 隐藏时，因为它还是会占用页面控件，所以会进行跳转
-->
```

## 预排版标签

```html
<!--
预排版标签中输入的内容不会被格式化，输入时的排版是怎样在网页中呈现的就是怎样
主要用于PHP打印结果
-->
<p>
    <pre>
                    上
        左                           右
                    下
    </pre>
</p>

```

## 图片标签

```html
<--! 宽高可以不带单位,利用宽高可以缩小或放大图片 -->
<img src="path" alt="资源不存在时显示的文字" title="鼠标悬浮时显示的文字" width="20px" height="20px">
```

## 实体

用于替换特殊字符（即HTML语法中会使用到的字符）的代码，实体不会被浏览器解析

### 带有实体名称的 ASCII 实体

| 结果 | 描述           | 实体名称 | 实体编号 |
| :--- | :------------- | :------- | :------- |
| "    | quotation mark | \&quot;  | \&#34;   |
| '    | apostrophe     | \&apos;  | \&#39;   |
| &    | ampersand      | \&amp;   | \&#38;   |
| <    | less-than      | \&lt;    | \&#60;   |
| >    | greater-than   | \&gt;    | \&#62;   |

### ISO 8859-1 符号实体

| 结果 | 描述                         | 实体名称  | 实体编号 |
| :--- | :--------------------------- | :-------- | :------- |
|      | non-breaking space           | \&nbsp;   | \&#160;  |
| ¡    | inverted exclamation mark    | \&iexcl;  | \&#161;  |
| ¢    | cent                         | \&cent;   | \&#162;  |
| £    | pound                        | \&pound;  | \&#163;  |
| ¤    | currency                     | \&curren; | \&#164;  |
| ¥    | yen                          | \&yen;    | \&#165;  |
| ¦    | broken vertical bar          | \&brvbar; | \&#166;  |
| §    | section                      | \&sect;   | \&#167;  |
| ¨    | spacing diaeresis            | \&uml;    | \&#168;  |
| ©    | copyright                    | \&copy;   | \&#169;  |
| ª    | feminine ordinal indicator   | \&ordf;   | \&#170;  |
| «    | angle quotation mark (left)  | \&laquo;  | \&#171;  |
| ¬    | negation                     | \&not;    | \&#172;  |
| ­    | soft hyphen                  | \&shy;    | \&#173;  |
| ®    | registered trademark         | \&reg;    | \&#174;  |
| ¯    | spacing macron               | \&macr;   | \&#175;  |
| °    | degree                       | \&deg;    | \&#176;  |
| ±    | plus-or-minus                | \&plusmn; | \&#177;  |
| ²    | superscript 2                | \&sup2;   | \&#178;  |
| ³    | superscript 3                | \&sup3;   | \&#179;  |
| ´    | spacing acute                | \&acute;  | \&#180;  |
| µ    | micro                        | \&micro;  | \&#181;  |
| ¶    | paragraph                    | \&para;   | \&#182;  |
| ·    | middle dot                   | \&middot; | \&#183;  |
| ¸    | spacing cedilla              | \&cedil;  | \&#184;  |
| ¹    | superscript 1                | \&sup1;   | \&#185;  |
| º    | masculine ordinal indicator  | \&ordm;   | \&#186;  |
| »    | angle quotation mark (right) | \&raquo;  | \&#187;  |
| ¼    | fraction 1/4                 | \&frac14; | \&#188;  |
| ½    | fraction 1/2                 | \&frac12; | \&#189;  |
| ¾    | fraction 3/4                 | \&frac34; | \&#190;  |
| ¿    | inverted question mark       | \&iquest; | \&#191;  |
| ×    | multiplication               | \&times;  | \&#215;  |
| ÷    | division                     | \&divide; | \&#247;  |

### ISO 8859-1 字符实体

| 结果 | 描述                         | 实体名称  | 实体编号 |
| :--- | :--------------------------- | :-------- | :------- |
| À    | capital a, grave accent      | \&Agrave; | \&#192;  |
| Á    | capital a, acute accent      | \&Aacute; | \&#193;  |
| Â    | capital a, circumflex accent | \&Acirc;  | \&#194;  |
| Ã    | capital a, tilde             | \&Atilde; | \&#195;  |
| Ä    | capital a, umlaut mark       | \&Auml;   | \&#196;  |
| Å    | capital a, ring              | \&Aring;  | \&#197;  |
| Æ    | capital ae                   | \&AElig;  | \&#198;  |
| Ç    | capital c, cedilla           | \&Ccedil; | \&#199;  |
| È    | capital e, grave accent      | \&Egrave; | \&#200;  |
| É    | capital e, acute accent      | \&Eacute; | \&#201;  |
| Ê    | capital e, circumflex accent | \&Ecirc;  | \&#202;  |
| Ë    | capital e, umlaut mark       | \&Euml;   | \&#203;  |
| Ì    | capital i, grave accent      | \&Igrave; | \&#204;  |
| Í    | capital i, acute accent      | \&Iacute; | \&#205;  |
| Î    | capital i, circumflex accent | \&Icirc;  | \&#206;  |
| Ï    | capital i, umlaut mark       | \&Iuml;   | \&#207;  |
| Ð    | capital eth, Icelandic       | \&ETH;    | \&#208;  |
| Ñ    | capital n, tilde             | \&Ntilde; | \&#209;  |
| Ò    | capital o, grave accent      | \&Ograve; | \&#210;  |
| Ó    | capital o, acute accent      | \&Oacute; | \&#211;  |
| Ô    | capital o, circumflex accent | \&Ocirc;  | \&#212;  |
| Õ    | capital o, tilde             | \&Otilde; | \&#213;  |
| Ö    | capital o, umlaut mark       | \&Ouml;   | \&#214;  |
| Ø    | capital o, slash             | \&Oslash; | \&#216;  |
| Ù    | capital u, grave accent      | \&Ugrave; | \&#217;  |
| Ú    | capital u, acute accent      | \&Uacute; | \&#218;  |
| Û    | capital u, circumflex accent | \&Ucirc;  | \&#219;  |
| Ü    | capital u, umlaut mark       | \&Uuml;   | \&#220;  |
| Ý    | capital y, acute accent      | \&Yacute; | \&#221;  |
| Þ    | capital THORN, Icelandic     | \&THORN;  | \&#222;  |
| ß    | small sharp s, German        | \&szlig;  | \&#223;  |
| à    | small a, grave accent        | \&agrave; | \&#224;  |
| á    | small a, acute accent        | \&aacute; | \&#225;  |
| â    | small a, circumflex accent   | \&acirc;  | \&#226;  |
| ã    | small a, tilde               | \&atilde; | \&#227;  |
| ä    | small a, umlaut mark         | \&auml;   | \&#228;  |
| å    | small a, ring                | \&aring;  | \&#229;  |
| æ    | small ae                     | \&aelig;  | \&#230;  |
| ç    | small c, cedilla             | \&ccedil; | \&#231;  |
| è    | small e, grave accent        | \&egrave; | \&#232;  |
| é    | small e, acute accent        | \&eacute; | \&#233;  |
| ê    | small e, circumflex accent   | \&ecirc;  | \&#234;  |
| ë    | small e, umlaut mark         | \&euml;   | \&#235;  |
| ì    | small i, grave accent        | \&igrave; | \&#236;  |
| í    | small i, acute accent        | \&iacute; | \&#237;  |
| î    | small i, circumflex accent   | \&icirc;  | \&#238;  |
| ï    | small i, umlaut mark         | \&iuml;   | \&#239;  |
| ð    | small eth, Icelandic         | \&eth;    | \&#240;  |
| ñ    | small n, tilde               | \&ntilde; | \&#241;  |
| ò    | small o, grave accent        | \&ograve; | \&#242;  |
| ó    | small o, acute accent        | \&oacute; | \&#243;  |
| ô    | small o, circumflex accent   | \&ocirc;  | \&#244;  |
| õ    | small o, tilde               | \&otilde; | \&#245;  |
| ö    | small o, umlaut mark         | \&ouml;   | \&#246;  |
| ø    | small o, slash               | \&oslash; | \&#248;  |
| ù    | small u, grave accent        | \&ugrave; | \&#249;  |
| ú    | small u, acute accent        | \&uacute; | \&#250;  |
| û    | small u, circumflex accent   | \&ucirc;  | \&#251;  |
| ü    | small u, umlaut mark         | \&uuml;   | \&#252;  |
| ý    | small y, acute accent        | \&yacute; | \&#253;  |
| þ    | small thorn, Icelandic       | \&thorn;  | \&#254;  |
| ÿ    | small y, umlaut mark         | \&yuml;   | \&#255;  |

## 表格

```html
<!--
border 属性只能放在 table 中，表示整个表格边框大小，不设置此属性则表格没有边框
width 属性表示整个表格的宽度
height 属性表示整个表格的高度
cellspacing 属性表示单元格之间的间距，默认是2px，设置为 0 则两条线合并
cellpadding 属性表示单元格填充（即文字的上下左右都填充的距离，默认为1）
align 属性表示表格整体的水平对齐方式，值有 left|right|cennter
每个单元格也可以单独设置 align 属性，不受单元格整体 align 属性的值影响
tr 也可以使用 align 属性，表示该行所有表格的对齐方式

tr 和 td 都可以加 valign 属性，表示垂直对齐方式，但 table 不能加

合并单元格
td 标签中使用 colspan="num" 合并列（左右合并）在左边的 td 中添加，num表示合并几列。
使用 rowspan="num" 合并行（上下合并）在上面的 td 中添加，num表示合并几行。
Tips：合并后一定要将多余的单元格(td)删掉

th 标签时表头，用于加粗
-->
<table border="1" cellspacing="0" cellpadding="20" align="center">
    <tr>
        <th>姓名</th>
        <th>年龄</th>
        <th>性别</th>
    </tr>
    <tr>
        <td>令狐冲</td>
        <td>22</td>
        <td>男</td>
    </tr>
    <tr>
        <td>任盈盈</td>
        <td>18</td>
        <td>女</td>
    </tr>
</table>
<!-- 表格中可以嵌套其他标签，用来格式化其他标签。例如表单 -->
```

## 排版标签

```html
<!-- 这两个标签都没有语义，可以存放任何东西，区别在于 div 会将包裹的内容换行，单行间距比 p 标签小。span 标签不会换行

一般将 div 标签用作盒子
span 一般只存放文字
-->
<div>一般用于存放图片、文字、视频等网页内容</div>
<span>一般只用于存放文字</span>
```

### 盒子模型

`div`：本质上是一个盒子，在网页排版过程中，主要就是对盒子模型的操作

盒子模型的特性：宽高、内间距（内填充）、外间距、边框

## 表单

```html
<!--
表单元素中，需要用户输入值时可以不加 value。不需要用户输入时，应该加 value
-->
<!-- 表单域 -->
<from>
    <!-- 表单元素 -->
    <!-- 文本框（单行文本域） -->
    <input type="text">
    <!-- 口令框（密码框） -->
    <input type="password">
    <!-- 单选框：同一组单选框都需要加 name 属性，且 name 属性的值必须保持一致。默认选中的属性是 checked 值也是 checked -->
    <input type="radio" name="sex" checked="checked">男
    <input type="radio" name="sex">女
    <!-- 多选框：默认选中的属性是 checked 值也是 checked-->
    <input type="checkbox">吃
    <input type="checkbox">喝
    <input type="checkbox" checked="checked">玩
    <input type="checkbox">乐
    <!-- 文件上传 -->
    <input type="file">
    <!-- 下拉框：默认选中属性是 selected 值也是 selected -->
    <select>
        <option>四川</option>
        <option>重庆</option>
        <option selected="selected">山西</option>
    </select>
    <!-- 文本域:不需要设置大小 -->
    <textarea rows="50" cols="50"></textarea>
    <!-- 提交按钮 -->
    <input type="submit">
    <!-- 提交按钮 -->
    <input type="button" value="点击一下">
    <!-- 提交按钮 -->
    <input type="reset">
    <!-- 提交按钮 -->
    <button>类似提交的按钮</button>
</from>


<!-- 分组的下拉框 -->
<select>
    <optgroup lable="省份">
        <option>山东省</option>
        <option>广东省</option>
        <option>山西省</option>
    </optgroup>
    <optgroup lable="行业">
        <option>开发</option>
        <option>测试</option>
        <option>运维</option>
    </optgroup>
</select>
```

## 上标和下标

```html
<sup>上标</sup>
<sub>下标</sub>
```

## 框架

```html
<!--
frameset 框架集标签，rows属性设置框架分为几行显示，每行占多少像素，星号表示剩下的全部。cols 属性设置框架分几列显示，每列占多少像素

frame 框架标签，src 属性用来指定要引入的页面
Tips：
   1. 框架页面中不能有 body 标签
   2. noframe 标签中可以有 body 标签，noframe 标签是当浏览器不支持框架集时显示的内容
   3. 框架集可以嵌套使用
-->
<frameset clos="200,*">
    <frame src="path" name="xxx">
    <frameset rows="300,*">
        <frame src="path" name="xxx">
        <frame src="path" name="xxx">
    </frameset>
</frameset>

<noframes>
    <body>
        框架丢失，请重试！！！
    </body>
</noframes>

<!-- 内嵌框架：用于 body 标签中，可以将其他页面嵌入到网页中 -->
<iframe src="path"></iframe>
```

## 多媒体标签

```html
<!--
embed：可以用来插入多媒体，支持的格式有：Mldl、Wav、Flac、AIFF、AU、Webm、MP3、MP4等
autostart=true|false：看之音视频是否自动播放
loop=正整数|true|false：用来控制音视频是否在结束后自动循环和循环次数
hidden=true|false：设置多媒体控制面板是否隐藏
-->
<emdeb src="path"></emdeb>


<!--
audio：用来插入音频。默认隐藏需要 controls 属性开启显示，autoplay 设置自动播放
还可以使用 source 子标签来定义多个源文件，当前面的源文件格式不支持时，依次往下查找
-->
<audio src="path" controls="controls" autoplay="autoplay"></audio>

<!--
video：用来插入视频。默认隐藏需要 controls 属性开启显示，autoplay 设置自动播放
还可以使用 source 子标签来定义多个源文件，当前面的源文件格式不支持时，依次往下查找
-->
<video src="path" controls="controls" autoplay="autoplay"></video>
<video>
    <source src="path">
    <source src="path">
</video>
```
