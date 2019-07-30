https://www.php-fig.org/psr/
- PSR-0 (Autoloading Standard) 自动加载标准 
- PSR-1 (Basic Coding Standard) 基础编码标准 
- PSR-2 (Coding Style Guide) 编码风格向导 
- PSR-3 (Logger Interface) 日志接口 
- PSR-4 (Improved Autoloading) 自动加载的增强版，可以替换掉PSR-0了。

## PSR0
不推荐使用 - 在2014年10月21日PSR-0已被标记为过时。PSR-4现在推荐作为替代。

> 1. 一个完全合格的namespace和class必须符合这样的结构：“\< Vendor Name>(< Namespace>)*< Class Name>”
> 1. 每个namespace必须有一个顶层的namespace（"Vendor Name"提供者名字）
> 1. 每个namespace可以有多个子namespace
> 1. 当从文件系统中加载时，每个namespace的分隔符(/)要转换成 DIRECTORY_SEPARATOR(操作系统路径分隔符)
> 1. 在类名中，每个下划线(_)符号要转换成DIRECTORY_SEPARATOR(操作系统路径分隔符)。在namespace中，下划线(_)符号是没有（特殊）意义的。
> 1. 当从文件系统中载入时，合格的namespace和class一定是以 .php 结尾的
> 1. verdor name,namespaces,class名可以由大小写字母组合而成（大小写敏感的）

## PSR1

> 1. PHP源文件必须只使用 <?php 和 <?= 这两种标签。
> 1. 源文件中php代码的编码格式必须是不带字节顺序标记(BOM)的UTF-8。
> 1. 一个源文件建议只用来做声明（类(class)，函数(function)，常量(constant)等）或者只用来做一些引起副作用的操作（例如：输出信息，修改.ini配置等）,但不建议同时做这两件事。
> 1. 命名空间(namespace)和类(class) 必须遵守PSR-0标准。
> 1. 类名(class name) 必须使用骆驼式(StudlyCaps)写法 (注：驼峰式(cameCase)的一种变种，后文将直接用StudlyCaps表示)。
> 1. 类(class)中的常量必须只由大写字母和下划线(_)组成。
> 1. 方法名(method name) 必须使用驼峰式(cameCase)写法。

## PSR2
1. 源文件
    1. 文件末尾必须空一行。
    2. 必须使用Unix LF(换行)作为行结束符。
    3. 纯PHP代码源文件的关闭标签?>必须省略。

第3点其实是蛮重要的，我之前还老写闭合，现在不写了。这可以避免在 PHP 结束标记之后万一意外加入了空格或者换行符，会导致 PHP 开始输出这些空白，而脚本中此时并无输出的意图。

2. 缩进

必须使用4个空格来缩进，不能使用Tab键。当然你如果把Tab在编辑器里手动设置为4个空格也可以。这样的目的是因为：每个人的机器上的Tab键都不一样，有些是4个空格，有些是8个空格，在你的机器上看着很爽的代码，在别人机器上了就各种恶心了。所以，统一搞成4个空格，不管在哪里打开都是美观的。

3. 行

一行推荐的是最多写80个字符，多于这个字符就应该换行了，一般的编辑器是可以设置的。

4. 关键字和 True/False/Null

php的关键字，必须小写，boolean值：true，false，null 也必须小写
> '__halt_compiler', 'abstract', 'and', 'array', 'as', 'break', 'callable', 'case', 'catch', 'class', 'clone', 'const', 'continue', 'declare', 'default', 'die', 'do', 'echo', 'else', 'elseif', 'empty', 'enddeclare', 'endfor', 'endforeach', 'endif', 'endswitch', 'endwhile', 'eval', 'exit', 'extends', 'final', 'for', 'foreach', 'function', 'global', 'goto', 'if', 'implements', 'include', 'include_once', 'instanceof', 'insteadof', 'interface', 'isset', 'list', 'namespace', 'new', 'or', 'print', 'private', 'protected', 'public', 'require', 'require_once', 'return', 'static', 'switch', 'throw', 'trait', 'try', 'unset', 'use', 'var', 'while', 'xor'

5. 命名空间(Namespace)和导入(Use)声明

    1. 命名空间(namespace)的声明后面必须有一行空行。
    1. 所有的导入(use)声明必须放在命名空间(namespace)声明的下面。
    1. 一句声明中，必须只有一个导入(use)关键字。
    1. 在导入(use)声明代码块后面必须有一行空行。
    
    
```
<?php
namespace Lib\Databases;  // 下面必须空格一行

use FooInterface;  //use 必须在namespace 后面声明
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass; //  下面必须空格一行

class Mysql 
{
}
```

6. 类(class)，属性(property)和方法(method)

    1. 继承(extends) 和实现(implement) 必须和 class name 写在一行，切花括号要换行写。
    
    ```
    <?php
    namespace Lib\Databaes;
    
    class Mysql extends ParentClass implements \PDO, \DB  // 写一行
    { //换行写{
    
    }
    
    ```
    
    2. 属性(property)必须声明其可见性，到底是 public 还是protected还是 private，不能省略，也不能使用var, var是php老版本中的什么方式，等用于public.
    
    3. 方法(method) ,必须 声明其可见性，到底是 public 还是protected还是 private，不能省略。并且，花括号{必须换行写。如果有多个参数，第一个参数后紧接, ,再加个空格，且函数name和( 之间必须要有个空格： function_name ($par, $par2, $pa3), 如果参数有默认值，也要用左右空格分开。
    
    ```
    <?php
    namespace Lib\Databaes;
    
    class Mysql extends ParentClass implements \PDO, \DB  // 写一行
    {
        public $foo = null;
        private $name = 'yangyi';
        protected $age = '17';
        
        public getInfo ($name, $age, $gender = 1) //函数名getInfo和(之间有个空格，参数之间也要有空格。默认参数也要左右都有空格
        { //必须换行写{
        
        }
    }
    ```
    
    4. 当用到抽象(abstract)和终结(final)来做类声明时，它们必须放在可见性声明 （public 还是protected还是 private）的前面。而当用到静态(static)来做类声明时，则必须放在可见性声明的后面。
    
    ```
    <?php
    namespace Vendor\Package;
    
    abstract class ClassName
    {
        protected static $foo;  //static放后面
        
        abstract protected function zim(); //abstract放前面
        
        final public static function bar() //final放前面，static放最后。
        {
            // 方法主体部分
        }
    }
    ```

7.控制结构

    1. if，elseif，else写法，直接上规范代码吧:
    
```
<?php
if ($expr1) { //左右空格
    // if body
} elseif ($expr2) { //elesif 连着写
    // elseif body
} else {
    // else body;
}
```
    2. switch，case 注意左右空格和换行，还是直接上规范代码：
    
```
<?php
switch ($expr) { //左右空格
    case 0:
        echo 'First case, with a break'; //对其
        break;  //换行写break ,也对其。
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```
    
    3. while，do while 的写法也是类似，要左右空格，上代码：
    
```
<?php
while ($expr) { //左右空格
    // structure body
}
do {
    // structure body;  //左右空格
} while ($expr);
```

    4 . for的写法
    
    
```
<?php
for ($i = 0; $i < 10; $i++) { //注意几个参数之间的空格
    // for body
}
```

    5 . foreach的写法
    
    
```
<?php
foreach ($iterable as $key => $value) { //还是空格问题
    // foreach body
}
```

    6 . try catch的写法
    
    
```
<?php
try {
    // try body
} catch (FirstExceptionType $e) { //同样也是注意空格。
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```


## PSR4

1. 废除了PSR-0中_就是目录分割符的写法，_下划线在完全限定类名中是没有特殊含义了。 
2. 类文件名要以 .php 结尾。 
3. 类名必须要和对应的文件名要一模一样，大小写也要一模一样。


    


