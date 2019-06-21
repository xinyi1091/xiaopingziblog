
---

title: 你所不知的 PHP 断言(assert)

date: 2019-06-04 01:19:12 +0800

tags: [语雀,PHP,travis CI]

categories: PHP

---

> PHP 中的断言常用于调试，检查一个表达式或语句是否为 FALSE。本文带你重新认识 PHP `assert()` 函数的神(Qi)通(Yin)广(Ji)大(Qiao)。
> 本文基于 PHP Version 7.1.28

[]()
<a name="243416d7"></a>
## 什么是断言

编写程序时，常会做出一定的假设，那断言就是用来捕获假设的异常，我们也可以认为断言是异常的一种特殊形式。

断言一般用于程序执行结构的判断，不可让断言处理业务流程。用的最多的场景就是单元测试，一般的单元测试框架都采用了断言。

```php
assert(1 == 2);

// 运行结果:
// Warning: assert(): assert(1 == 2) failed in /Users/shocker/Desktop/demo.php on line 25
```

[]()
<a name="25045823"></a>
## PHP 中的断言

在 PHP 中，采用 [assert()](https://www.php.net/manual/zh/function.assert.php) 函数对表达式进行断言。

```php
// PHP 5
assert ( mixed $assertion [, string $description ] ) : bool

// PHP 7
assert ( mixed $assertion [, Throwable $exception ] ) : bool
```

[]()
<a name="82770988"></a>
### 传统的断言方式 (PHP 5 & 7)

> 参数 assertion 既支持表达式，也支持表达式字符串（某些特定的场景会用到，比如判断某个字符串表达式是否合法）


如果 assertion 是字符串，它将会被 `assert()` 当做 PHP 代码来执行。assertion 是字符串的优势是当禁用断言时它的开销会更小，**并且在断言失败时消息会包含 assertion 表达式**。

断言这个功能应该只被用来调试。你应该用于完整性检查时测试条件是否始终应该为 TRUE，来指示某些程序错误，或者检查具体功能的存在（类似扩展函数或特定的系统限制和功能）。

断言不应该用于普通运行时操作，类似输入参数的检查。作为一个经验法则，在断言禁用时你的代码也应该能够正确地运行。

**使用示例:**

```php
function my_assert_handler($file, $line, $code, $desc)
{
    echo "Assertion Failed:
    File '{$file}'
    Line '{$line}'
    Code '{$code}'
    Desc '{$desc}'
";
}

// 设置回调函数
assert_options(ASSERT_CALLBACK, 'my_assert_handler');

// 让一则断言失败
assert('1 == 2', '1 不可能等于 2');
```

**运行结果:**

```php
Assertion Failed:
    File '/Users/shocker/Desktop/demo.php'
    Line '29'
    Code '1 == 2'
    Desc '1 不可能等于 2'
```

[]()
<a name="19d9d227"></a>
### 支持异常的断言 (仅 PHP 7)

在 PHP 7 中，`assert()` 是一个语言结构，允许在不同环境中生效不同的措施，具体可见 [zend.assertions](https://www.php.net/manual/zh/ini.core.php#ini.zend.assertions) 配置。

另外，还支持通过 [AssertionError](https://www.php.net/manual/en/class.assertionerror.php) 捕获错误。

**使用示例:**

```
assert_options(ASSERT_EXCEPTION, 1); 

try {
    
    assert(true == false, new AssertionError('True is not false!'));
} catch (Throwable $e) {
    echo $e->getMessage();
}
```

**运行结果:**

```
True is not false!
```

[]()
<a name="a2b3052b"></a>
## 对断言行为进行控制
PHP 支持 [assert_options()](https://www.php.net/manual/zh/function.assert-options.php) 函数对断言进行配置，也可用 ini 进行设置

> 以下配置中，常量标志用于 `assert_options()` 函数进行配置，ini 设置用于 `ini_set()` 函数设置，效果一样
> 

| 标志 | INI 设置 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| ASSERT_ACTIVE | assert.active | "1" | 启用 `assert()` 断言 |
| ASSERT_WARNING | assert.warning | "1" | 为每个失败的断言产生一个 PHP 警告（warning） |
| ASSERT_BAIL | assert.bail | "0" | 在断言失败时中止执行 |
| ASSERT_QUIET_EVAL | assert.quiet_eval | "0" | 在断言表达式求值时禁用 error_reporting |
| ASSERT_CALLBACK | assert.callback | NULL | 断言**失败时**调用该回调函数 |
| ASSERT_EXCEPTION | assert.exception | "0" | 在断言失败时产生 [AssertionError](https://www.php.net/manual/en/class.assertionerror.php) 异常 （自 PHP 7.0.0 起有效） |


在断言失败时产生 [AssertionError](https://www.php.net/manual/en/class.assertionerror.php) 异常 （自 PHP 7.0.0 起有效）

`zend.assertions` 是个特殊的配置（PHP >= 7.0.0 支持），**控制不同运行环境下断言的行为**，仅可用 `ini_set()` 进行设置。并且，设置了`1`就不能再设置为`-1`，反之亦然，其他不受限。

> - **1**: 编译代码，并执行(开发模式)
> - **0**: 编辑代码，但运行时跳过
> - **-1**: 不编译代码(生产模式)


[]()
<a name="4277a863"></a>
## 版本的不兼容

- PHP >= 5.4.8，description 可作为第四个参数提供给 ASSERT_CALLBACK 模式里的回调函数
- 在 PHP 5 中，参数 assertion 必须是可执行的字符串，或者运行结果为布尔值的表达式
- 在 PHP 7 中，参数 assertion 可以是任意表达式，并用其运算结果作为断言的依据
- 在 PHP 7 中，参数 exception 可以是个 [Throwable](https://www.php.net/manual/en/class.throwable.php) 对象，用于捕获表达式运行错误或断言结果为失败。(当然 [assert.exception](https://www.php.net/manual/zh/info.configuration.php#ini.assert.exception) 需开启)
- PHP >= 7.0.0，支持 `zend.assertions`、`assert.exception` 相关配置及其特性
- PHP >= 7.2 版本开始，参数 assertion 不再支持字符串
> 详见 [PHP 7.2.x 中废弃的功能](https://www.php.net/manual/zh/migration72.deprecated.php)

```
Deprecated: assert(): Calling assert() with a string argument is deprecated
```


[]()
<a name="3dbf0c11"></a>
## 应用场景

[]()
<a name="0f3d3b03"></a>
### 调试输出

**先看示例:**

```
assert('1 == 2', '1 不可能等于 2');
```

**运行结果:**

```
Warning: assert(): 1 不可能等于 2: "1 == 2" failed in /Users/shocker/Desktop/demo.php on line 10
```

**类似于:**

```
$expression = 1 == 2;
if (!($expression)) {
    echo "1 不可能等于 2\n";
    var_dump($expression);
    echo __FILE__ . "\n";
}
```

但是，我们无法得知 $expression 的具体表达式，也无法得知具体的执行行数。

[]()
<a name="93b824b5"></a>
### 单元测试

```
function arraySum(array $nums) {
    $sum = 0;
    foreach ($nums as $n) {
        $sum += $n;
    }

    return $sum;
}

assert(arraySum([1, 2, 3]) == 6, 'arraySum() 测试不通过:');
assert(is_numeric(arraySum([1, 2, 3])), 'arraySum() 测试不通过:');
```

是不是跟我们用 [PHPUnit](https://phpunit.de/) 写单元测试很像😆

[]()
<a name="ef0df9dd"></a>
### 验证表达式

> **Tip:**
> PHP 7 开始，新增了 [Error](https://www.php.net/manual/en/class.error.php) 类用于捕获 PHP 内置错误，包括语法错误。Error 与之前的 Exception 均继承自 [Throwable](https://www.php.net/manual/en/class.throwable.php)，所以从 7.0.0 开始，Throwable 可以捕获一切错误和异常。


下例演示了如何验证某个字符串表达式是否为合法的 PHP 表达式:

```
try {
    assert('a +== 1');
} catch (Throwable $e) {
    echo $e->getMessage(), "\n";
}
```

**运行结果:**

```
Failure evaluating code: 
a +== 1
```

[]()
<a name="a6d02942"></a>
## 安全问题

假设是下列代码，会有什么结果呢？

```
function demo(){
    file_put_contents('data.log', 'shockerli.net');
    return true;
}

$func = $_GET["func"];
assert("$func()");
```

所以，对于 assert 函数，正常情况下是不建议用于生产环境的。

与 eval 一样会执行任何 PHP 代码，危害极大。这也是 PHP 从 7.2 开始废弃支持字符串表达式的原因。

---

> 感谢您的阅读，觉得内容不错，点个赞吧 😆<br />
原文地址: [https://shockerli.net/post/php-assert/](https://shockerli.net/post/php-assert/?source=segmentfault)


