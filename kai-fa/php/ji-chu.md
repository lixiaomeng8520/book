# 基础

## 参考

* [PHP 7 错误处理](http://php.net/manual/zh/language.errors.php7.php)

## Error 和 Exception

php7以后，Error 和 Exception 都继承自 Throwable， 所以都可以被捕获。

## 重载

PHP所提供的"重载"（overloading）是指动态地"创建"类属性和方法。我们是通过魔术方法（magic methods）来实现的。

当调用当前环境下未定义或不[可见](http://php.net/manual/zh/language.oop5.visibility.php)的类属性或方法时，重载方法会被调用。本节后面将使用"不可访问属性（inaccessible properties）"和"不可访问方法（inaccessible methods）"来称呼这些未定义或不可见的类属性或方法。

所有的重载方法都必须被声明为 _public_。

### 属性重载

| 方法 | 调用时机 |
| --- | --- | --- | --- | --- |
|  [\_\_set\(\)](http://php.net/manual/zh/language.oop5.overloading.php#object.set) | 在给不可访问属性赋值时 |
|  [\_\_get\(\)](http://php.net/manual/zh/language.oop5.overloading.php#object.get) | 读取不可访问属性的值时 |
|  [\_\_isset\(\)](http://php.net/manual/zh/language.oop5.overloading.php#object.isset) | 当对不可访问属性调用 [isset\(\)](http://php.net/manual/zh/function.isset.php) 或 [empty\(\)](http://php.net/manual/zh/function.empty.php) 时 |
|  [\_\_unset\(\)](http://php.net/manual/zh/language.oop5.overloading.php#object.unset) | 当对不可访问属性调用 [unset\(\)](http://php.net/manual/zh/function.unset.php) 时 |

### 方法重载

| 方法 | 调用时机 |
| --- | --- | --- |
|  [\_\_call\(\)](http://php.net/manual/zh/language.oop5.overloading.php#object.call) | 在对象中调用一个不可访问方法时 |
|  [\_\_callStatic\(\)](http://php.net/manual/zh/language.oop5.overloading.php#object.callstatic) | 在静态上下文中调用一个不可访问方法时 |

