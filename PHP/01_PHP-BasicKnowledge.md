## PHP基本格式

```php
 <?php
 // 每行代码以分号结尾
 PHP代码
 ?>
```

## 注释

```php
<?php
// 单行注释
# 单行注释

/**
* 多行注释
*/
?>
```

## 变量

```php
<?php
// php是一门弱类型语言，变量的定义可以随用随定义。以 $ 符号开始，后面跟下划线、字母、数字
// 不可以以数字开头
$name = "leon";
echo $name;

// 可变变量
$name = "leon";
$$name = "lily";
echo $leon;
// $leon 的值是 lily，双 $ 符定义的是可变变量，变量名是单 $ 符的值

// 静态变量
<?php
function make()
{
    /** static 用于将变量在内存中持久化，此时 $num的值在初始化后，每一次执行make函数时，不再		* 初始化 $num的值，$num的值会一直累加
    */
    static $num = 1;
    $num = $num + 1;
    return $num.'<hr/>';
}
echo make();
echo make();
echo make();

?>
```

## 变量作用域

### 全局变量

```php
<?php
// 获取全局变量的两种方式
$name = "leon";
function show()
{
    // 使用global关键字定义全局变量
    global $name;
    echo $name;
}

function showOne()
{
    /** 
     * 使用php自带的全局变量方法获取
     * 单独打印 print_r($GLOBALS) 会打印出php自带的所有全局变量，也可以使用此变量来将普通变	 * 量变为全局变量 
     */
    echo $GLOBALS['name']
}
?>
```

## 变量检测与删除

```php
<?php
// 检测变量是否存在，var_dump()用于打印类型，isset()返回的是 false 或 true
var_dump(isset($name))
// 删除变量
$name = "leon";
unset($name)
// 在函数体内无法删除全局变量
?>
```

## 赋值与传址

```php
<?php
// 赋值
$a = 1;
$b = $a;
$a = 3;
// 此时 $a 的值是3 $b 的值还是 1

// 传址
$a = 1;
$b = &$a;
$a = 3;
// 此时 $a 的值为 3 $b 的值也是3，使用 & 符号传递的是 $a 的内存地址，所以改变 $a 的值，	// $b 的值也发生改变
?>
```

## 数据类型

分类：

1. `string`：字符串
2. `integer`：整型
3. `float`：浮点型 
4. `array`：数组
5. `object`：对象
6. `boolean`：布尔类型

### 布尔型

1. 0 在php中可以表示 false，非0 为 true
2. 空字符串和空数组为 false
3. null 为 false
4. 对象即使是空也为 true

### 字符串

使用单引号或双引号包裹，单引号内不可以引用变量，双引号内部可以引用变量，使用大括号包裹

```php
<?php
$name = 'leon';
echo "my name is {$name}";
// 转义字符
echo "定义变量的方法：\$string = 10\;";
?>
```





























