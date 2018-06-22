# Pimple

> 原文地址：[https://pimple.symfony.com/](https://pimple.symfony.com/)

Pimple是一个小型的PHP依赖注入容器。

## 安装

使用composer：

```bash
php composer.phar require pimple/pimple ~3.0
```

作为PHP扩展：

```bash
git clone https://github.com/silexphp/Pimple
cd Pimple/ext/pimple
phpize
./configure
make
make install
```

## 使用

创建实例：

```php
use Pimple\Container;
$container = new Container();
```

和其他依赖注入容器一样，Pimple管理两种数据：服务和参数。

### 定义服务

服务是一个对象，在一个大型系统里的一部分。比如：数据库连接，模板引擎，邮件收发等。几乎所有全局对象都可以作为服务。

服务被定义为一个匿名函数，并返回一个对象实例：

```php
// define some services
$container['session_storage'] = function ($c) {
    return new SessionStorage('SESSION_ID');
};

$container['session'] = function ($c) {
    return new Session($c['session_storage']);
};
```

注意匿名函数可以访问当前容器实例，可以引用其他服务或参数。因为对象只在你获取他们的时候创建，所以定义的顺序不重要。

使用定义过的服务也很简单：

```php
// get the session object
$session = $container['session'];

// the above call is roughly equivalent to the following code:
// $storage = new SessionStorage('SESSION_ID');
// $session = new Session($storage);
```

### 定义工厂服务

默认情况下，每次获取服务时，Pimple都会返回相同的实例。如果你想要每次返回的不同，请在匿名函数歪包含`factory`函数。

```php
$container['session'] = $container->factory(function ($c) {
    return new Session($c['session_storage']);
});
```

现在，每次调用`$container['session']`都会返回session类的一个新实例。

### 定义参数

定义参数允许简化容器外部的配置，还可以存储全局变量：

```php
// define some parameters
$container['cookie_name'] = 'SESSION_ID';
$container['session_storage_class'] = 'SessionStorage';
```

如果你像这样更改`session_storage`服务定义：

```php
$container['session_storage'] = function ($c) {
    return new $c['session_storage_class']($c['cookie_name']);
};
```

你可以通过重写`session_storage_class`参数来轻松的修改cookie名字，而不是重新定义服务。

### 保护参数

因为Pimple把匿名函数当做服务定义，你需要在匿名函数包上`protected()`方法来把他们作为参数：

```php
$container['random_func'] = $container->protect(function () {
    return rand();
});
```

### 修改服务

有时候在定义过服务后想要修改它，你可以使用`extend()`方法来定义额外要运行的代码：

```php
$container['session_storage'] = function ($c) {    
    return new $c['session_storage_class']($c['cookie_name']);
};

$container->extend('session_storage', function ($storage, $c) {
    $storage->...();
    return $storage;
});
```

第一个参数是想要扩展的服务的名字，第二个函数来访问对象实例和容器。

### 扩展容器

如果你总是使用相同的库，你也许想在项目之间复用这些服务，那么就通过继承 `Pimple\ServiceProviderInterface`打包你的服务到`provider`：

```php
use Pimple\Container;
class FooProvider implements Pimple\ServiceProviderInterface
{
    public function register(Container $pimple)
    {
        // register some services and parameters
         // on $pimple
    }
}
```

然后，在容器上注册这个provider：

```php
$pimple->register(new FooProvider());
```

### 获取服务定义方法

当你想访问一个对象，Pimple会自动调用匿名函数，它会给你创建一个服务对象。如果你想获取这个函数的原始访问，可以调用`raw()`方法：

```php
$container['session'] = function ($c) {
    return new Session($c['session_storage']);
};

$sessionFunction = $container->raw('session');
```



