## 面向对象

将各种代码实现的功能通过类(Class)的方式封装起来，使代码重用性更高，代码结构清晰

## 结构

类中有方法和属性

- 方法：即函数，是代码实现的某一个具体功能
- 属性：即变量，是类中使用的变量或常量

## 实例讲解

### 静态变量、常量和静态方法

```php
<?php
// 使用 class ClassName{} 关键字定义一个类，定义时`ClassName`采用帕斯卡命名法，即首字母大写
class User{
    // 普通变量：属于私有属性，每个对象的该属性的值都不同，使用 $this 访问
    protected $name;
    // 静态变量：类中的静态变量和普通变量不同，静态变量属于公共属性，只能使用类来访问
    protected static $age = 18;
    // 类常量，一般全大写
    // 类常量的值不会被改变，要访问类常量必须使用类名或self
    const EXISTS_VALIDATE =1;
    public function say(){
        // 访问静态变量时只能使用 类名加冒号的方式访问。此时变量名前需要加 $ 符号
        return  '我已经' . User::$age . '岁了';
    }
    public function sayHi(){
        // 使用类名访问静态变量，如果类名发生了改变，也需要修改相应的调用静态变量的地方
        // 所以为了方便可以使用 self 代替当前类名
        // sefl 是指向当前类名的指针
        return  '我已经' . self::$age . '岁了';
    }
    public function setName(string $name){
        // $this：当前对象的指针，指向的是当前的对象而不是类
        // 访问变量时需要使用 $this 来进行访问，表示当前对象
        // 使用 $this 访问变量时，变量名前不用加 $ 符号
        $this->name =  $name;
    }
    public function getName(){
        return $this->name;
    }
    // 静态方法，如果一个方法不需要对象进行调用，只是用于类内部的其他方法调用时可以定义为静态方法
    // 静态方法中不能使用 $this 关键字，因为它是服务于类中的其他方法，而不是对象，但在外部还是可以通过对象调用静态类
    // 静态方法的执行效率高于普通方法
    public static function getAge(){
        return self::$age;
    }
    public function validate()
    {
        // 在类的内部访问类常量时使用 self 关键字
        return self::EXISTS_VALIDATE;
    }

}
// 使用 new className; 生成初始化一个对象
$leon = new User;
// 对象可以使用 -> 方式调用类中的方法
$leon->setName('leon');
echo $leon->getName();
echo '<hr/>';
// 调用静态方法时，只能使用类名进行调用
echo User::getAge();
echo '<hr/>';
// 在类的外部访问类常量使用类名访问
echo User::EXISTS_VALIDATE;
echo '<hr/>';
echo (new User)->validate();
echo '<hr/>';
// 在外部使用对象调用静态方法
echo $leon->getAge();
echo '<hr/>';
// 在外部使用类调用静态方法
echo User::getAge();
?>

```

### 继承和重写

```php
<?php
// adstract 用于定义抽象类或方法
abstract class Notify{
    protected $color = 'red';
    protected $credit = 3;
    // 定义一个抽象方法，只能在抽象类中定义
    // 抽象方法在父类中不会有具体的实现代码，抽象方法的具体实现在继承了此抽象类的子类中进行实现
    abstract public function content();
    // final 关键字，用于保护父类中的方法，防止子类重写此方法
    // 如果子类中重写了此方法就会报错
    public final function message()
    {
        // 父类中定义的属性($this->color)也会在子类中生效
        // 此处调用抽象方法 content()
        return '<span style="color:' . $this->color . '">
        '. $this->content() . '发送通知,奖励' . $this->credit() . '个积分</span>';
    }
    public function credit()
    {
        return $this->credit;
    }
    public function sendText()
    {
        return "我是父类中可以被重写的方法";
    }
}
// 使用 extends 关键字，可以继承父类
class User extends Notify{
    public function register()
    {
        // 继承后子类中可以直接调用父类中的方法
        return $this->message();
    }
    // 重写父类的方法，比如新老用户签到积分奖励不同，利用重写覆盖掉父类中的同名方法
    // 代码在调用时会先在当前类中查找是否有对应的方法，如果没有再去父类中查找。所以可以重写
    public function credit()
    {
        return 20;
    }
    // 如果子类继承的父类中有抽象方法，子类中必须进行实现
    public function content()
    {
        return;
    }
}
class Comment extends Notify{
    // 重写父类中的属性，和重写方法一样
    // 代码在执行时会先在当前类中查找，没有再去父类中查找
    protected $credit = 10;
    public function send()
    {
        return $this->message();
    }
    // 实现父类中的抽象方法
    public function content()
    {
        return "感谢你的评论，";
    }
    public function sendText()
    {
        // 重写父类的方法时会覆盖掉父类中的实现
        // 为了既能重写该方法，同时父类中原本的实现代码还是能正常执行，使用 parent 来调用被重写的方法
        // 重写后的代码可以在调用之前，也可以在调用之后，这样就不怕覆盖掉原本的实现了
        return parent::sendText();
    }
}

echo (new User)->register();
echo '<hr/>';
echo (new Comment)->send();
?>

```

### 保护类中的方法和属性

```php
<?php
class Notify{
    // public 定义的是公共方法，类和对象都可以调用，可以不写，默认就是 public
    public function normal()
    {
        return '我是父类里的公共方法';
    }
    // protected 关键字定义的受保护的方法，只能在当前类中使用，或子类中使用，对象无法调用
    protected function send()
    {
        return 'Notify send';
    }
    // private 关键字定义的私有方法，只能在当前类中使用，子类和对象都无法调用
    private function get()
    {
        return 'Notify get';
    }
}
class User extends Notify{
    public function say()
    {
        // 子类调用父类中 protected 定义的受保护的方法
        return '我是公共方法' . $this->send();
    }
}
$user = new User;
// 因为 say() 是公共方法，所以对象可以调用
// 虽然受保护的方法，对象无法调用，但因为子类中的公共方法调用了父类受保护的方法，所以可以正常输出不会报错
echo $user->say();
echo '<hr/>';
// 公共方法，对象也可以调用
echo $user->normal();
?>
```

### 多重继承

```php
<?php
trait SiteName
{
    public function getSiteName()
    {
        return 'baidu.com';
    }
}
// 当一个类继承多个父类时，称为多重继承，低版本的 PHP 中没有此功能，高版本中可以使用 trait 和 use 变相实现
// 使用 trait 关键字，定义可以被多重继承的类
trait Log
{
    public function save()
    {
        return __METHOD__;
    }
    // 也可以在 trait 类中定义抽象方法
    abstract public function name();
    // 也可以定义静态方法
    public static function show()
    {
        return 'show...static';
    }
}
trait Comment
{
    // 在 trait 类中也可以继承其他的 trait 类
    use SiteName;
    public function total()
    {
        return __METHOD__;
    }
    // 当两个 trait 类中存在同名方法时，在子类中要处理掉这个重名问题，否则报错
    public function save()
    {
        return __METHOD__;
    }
}
trait Protect
{
    // 使用 public 关键字定义的普通方法可以在子类中使用 as 改写为保护方法，禁止外部访问
    public function user()
    {
        return __FUNCTION__;
    }
    // 使用 protected 定义的方法无法被外部访问，用于保护方法
    // 不仅在 trait 定义的类中可以使用此关键字，普通类中也可以使用此关键字保护方法不被外部访问
    protected function log()
    {
        return __FUNCTION__;
    }
}
// 定义一个普通类
class Site
{

    public function total()
    {
        return __FUNCTION__;
    }
}
// 当使用 extends 继承的父类和使用 use 继承的 trait 父类中有同名方法时，trait 定义的父类优先级高于 extends 继承的父类
class Topic extends Site
{
    // 让子类继承多个父类
    // 只能继承由 trait 定义的父类
    // 此处继承了 Comment 类，而 Comment 类又继承了 SiteName 类，所以也继承了 SiteName 类
    use Log, Comment, Protect {
        // 当 trait 中存在重名方法时，在子类中使用 insteadof 关键字，定义默认使用哪一个父类中方法
        // 当设定了默认方法后，另一个父类中的重名方法就无法使用了
        Log::save insteadof Comment;
        // 如果还是想使用另一个父类中的重名的方法，可以使用 as 关键字重命名该方法
        Comment::save as send;
        // 在子类中保护父类中的普通方法，禁止外部访问
        Protect::user as protected;
    }
    // 继承的 Log 类中有一个抽象方法，因此子类中必须实现这个抽象方法
    public function name()
    {
    }
}

$topic = new Topic;
echo $topic->save();
echo '<hr/>';
// 此时调用要使用重名名后的方法名
echo $topic->send();
echo '<hr/>';
// 此时调用的是 Comment 类中的 total 方法，因为 trait 的优先级高于 extends 继承的父类
echo $topic->total();
echo '<hr/>';
// 继承的 Comment 类继承了 SiteName 类，相当于也继承了 SiteName 类，所以可以直接调用 SiteName 类中的方法
echo $topic->getSiteName();
echo '<hr/>';
// 调用其中的静态方法
echo $topic->show();
echo '<hr/>';
// 通过类名的方式调用静态方法
echo Topic::show();
?>

```

### 接口

```php
<?php
// 使用 interface 关键字定义一个接口类
// 接口类有点类似于一个抽象类，不同的是抽象类中不仅有抽象方法也可以有属性和实现的方法，接口类中只有抽象方法
interface InterFaceCache{
    // 接口中只有抽象方法
    public function set($name, $value);
    // 当抽象方法中设定了传递参数时，子类在实现该方法时也必须传递参数
    // 如果没有，则实现时也没有参数
    public function get ($name);
}
// implements 关键字用于继承接口类
// 继承一个接口类后，必须在类中实现接口类中定义的所有抽象方法
class Mysql implements InterFaceCache{
    // 实现接口中的抽象方法
    public function set($name, $value)
    {}
    // 子类在实现抽象方法时，如果抽象方法设定了参数，则实现时也必须传递参数
    public function get($name)
    {}
}
class Redi implements InterFaceCache{
    public function set($name, $value)
    {}
    public function get($name)
    {}
}
// 定义一个普通类
class Cache{
    // 定义一个静态方法，根据驱动不同选择不同的类生成对象
    public static function instance(string $driver)
    {
        switch (strtolower($driver)) {
            case 'mysql':
                return new Mysql;
            case 'redis':
                return new Redi;
        }
    }
}

$cache = Cache::instance('mysql');

var_dump($cache);
// 调用时必须传递参数
 var_dump($cache->get('test'));

?>
```

### 构造方法和析构方法

> 在 PHP 中，前面带两个下划线的方法，被称为魔术方法，是 PHP 的内置方法
>
> 魔术方法分为构造方法和析构方法
>
> 构造方法和析构方法刚好一个是对象刚刚实例化时和对象销毁时

```php
<?php


class Code{
    protected $width;
    // 构造方法是在实例化一个对象时会自动执行的方法
    // 构造函数一般会传递参数进行处理，可以给它设置默认值
    public function __construct(int $width=300)
    {
        echo '我是构造函数自动执行的输出' . '<hr/>';
        $this->width = $width;
    }
    public function make()
    {
        return '你生成了' . $this->width . '宽度的验证码';
    }
    // 实例化一个对象实际上是对类的引用
    // 析构函数在所有引用消失时会自动执行，即实例化的对象不再使用时，析构函数会自动执行
    // 例如当对象使用完毕后自动删除无效文件，如 session文件
    public function __destruct()
    {
        echo '<hr/>' . 'destruct';
    }
}
// 实例化对象时，构造函数会自动执行，实例化对象时，向类传递的参数会直接传给构造函数
// 不传参时使用默认值，传参使用传递的值
$code = new Code(100);
echo $code->make();
?>
```
