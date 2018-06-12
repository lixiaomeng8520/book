# 第一个应用

如果你想通过一个很简单的Slim应用学习到所有的相关知识，那么请阅读本章节。可以通过教程来构建简单应用，也可以根据需求调整每一个步骤。

在开始之前：有一个骨架项目让你快速入门。

> 这篇教程介绍一个示例应用。访问[这里](https://github.com/slimphp/Tutorial-First-Application)来参考它。

## 设置

首先为项目创建一个目录（这里叫做`project`，因为起名字真的很难）。我喜欢顶级目录没有代码，里面有一个源代码目录，源代码目录里创建一个项目根目录，所以目录结构是这样：

```text
.
├── project
│   └── src
│       └── public
```

### 安装Slim框架

Composer是安装Slim框架最好的方式。如果还没有Composer，你可以参考[安装指南](https://getcomposer.org/download/)，在我的项目里，我把`composer.phar`下载到`src/`目录里，可以在本地使用它。所以我的第一个命令是这样的（现在在`src/`目录）：

```text
php composer.phar require slim/slim
```

这条命令做了两件事：

* 添加Slim框架依赖到`composer.json`文件里（在我的例子里，因为我没有这个文件，所以它给我创建了一个；如果你已经有了`composer.json`文件，这条命令是安全的）
* 执行`composer install`，下载依赖，以便这些依赖在你的应用里确实可用

如果你现在查看项目目录，你将会看到一个`vendor`目录，里面有所有的库文件。还有两个新文件：`composer.json`和`composer.lock`。这也是我们代码控制的好时机：当使用composer，我们要排除`vendor/`目录，但是`composer.json`和`compooser.lock`这两个文件应该包含在代码控制里。因为我使用了`composer.phar`，所以也要把它包含在仓库里；你可以在所有需要它的系统里安装`composer`命令。

为了正确设置git排除，创建一个文件`src/.gitingore`，然后添加如下代码：

```text
vendor/*
```

现在git不会提示你把`vendor/`下的文件添加到仓库 - 我们不想这样做是因为使用composer来控制这些依赖比把它们包含在代码控制仓库里要好得多。

### 创建应用

在项目首页有一个很有优秀精简的Slim框架的`index.php`示例，我们使用它作为起点。将下面的代码添加到`src/public/index.php`文件里：

```php
<?php
use \Psr\Http\Message\ServerRequestInterface as Request;
use \Psr\Http\Message\ResponseInterface as Response;

require '../vendor/autoload.php';

$app = new \Slim\App;
$app->get('/hello/{name}', function (Request $request, Response $response, array $args) {
    $name = $args['name'];
    $response->getBody()->write("Hello, $name");

    return $response;
});
$app->run();
```

我们仅仅粘贴了这些代码 ... 让我们看看它做了什么。

脚本最上面的`use`指令仅仅把`Request`和`Response`类引进我们的脚本，这样我们就不用通过他们冗长的名字来引用它。Slim框架支持PSR-7（PHP的HTTP消息标准），所以你会注意到，当你构建应用的时候，你会经常看到`Request`和`Response`对象。这是写web应用程序非常先进而且优秀的方法。

第二步我们包含`vendor/autoload.php`文件 - 它是Composer创建的，允许我们引用之前创建的Slim和其他相关依赖。请注意，如果你使用和我相同的文件结构，那么`verdor/`目录是`index.php`文件的上一级，你需要像我做的一样调整路径。

最后我们创建`$app`对象，它是我们Slim善良的开始。`$app->get()`调用是我们的第一个“路由” - 当我们生成一个GET请求到`/hello/someone`，那么这就是响应它的代码。别忘记最后`$app->run`这行，告诉Slim我们已经配置好，可以继续主活动了。

现在我们完成了应用程序，我们需要运行它。有两种方式：PHP内置web服务器，或Apache虚拟主机。

### 使用PHP内置服务器来运行

这是我更喜欢的“快速启动”选项，因为它不依赖任何其他东西！在`src/public`目录里执行下面的命令：

```text
php -S localhost:8080
```

可以通过[http://localhost:8080来访问应用（如果你本机已经使用了8080端口，会被警告。只需要换一个不同的端口即可，PHP并不关心具体绑定到哪里）。](http://localhost:8080来访问应用（如果你本机已经使用了8080端口，会被警告。只需要换一个不同的端口即可，PHP并不关心具体绑定到哪里）。)

注意访问这个URL会提示“Page Not Found” - 但是这个错误提示来自Slim，所以这是正常的。尝试替换为Http://localhost:8080/hello/joebloggs :\)。

### 使用Apache或Nginx来运行

为了让它建立在一个标准LAMP栈，我们需要一些额外的东西：一些主机配置和一个重写规则。

虚拟主机的配置应该很简单；我们不需要其他特殊的东西。复制默认存在的配置，然后设置你想如何访问项目的ServerName。比如可以这样：

```text
ServerName slimproject.test
or for nginx:
server_name slimproject.test
```

然后把DocumentRoot指向public/目录：

```text
DocumentRoot /home/lorna/projects/slim/project/src/public/
or for nginx:
root /home/lorna/projects/slim/project/src/public/
```

不要忘记重启服务！

在src/public目录下还有一个.htaccess文件；它依赖于Apache的重写模块，可以简单的使所有的web请求转向index.php文件，这样Slim就可以为我们处理所有的路由。这是.htaccess内容：

{% code-tabs %}
{% code-tabs-item title=".htaccess" %}
```text
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule . index.php [L]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

nginx不使用.htaccess文件，所以你需要将下面代码添加到你的服务器配置的location块：

```text
if(!-e $request_filename){
    rewrite ^(.*)$ /index.php break;
}
```

注意：如果想入口文件是其他文件而不是index.php，你需要更改上面的配置。api.php经常作为入口文件，所以你的设置需要对应。这个例子假设你使用index.php。

使用这个设置，那么在教程的其他例子里，请使用[http://slimproject.test代替http://localhost:8080。同样会有警告：你会在http://slimproject.test看到错误页面，它是Slim的产生的。可以访问http://slimproject.test/hello/joebloggs。](http://slimproject.test代替http://localhost:8080。同样会有警告：你会在http://slimproject.test看到错误页面，它是Slim的产生的。可以访问http://slimproject.test/hello/joebloggs。)

## 配置和自动加载

现在我们已经搭建好了框架，我们可以在应用本身获取到我们想要的一切。

### 添加配置到应用

初始示例应用使用Slim的默认配置，但是当我们创建它的时候，可以轻松的添加配置。添加配置有不同的方法，这里我创建了一个配置数组，然后当创建Slim的时候，告诉它去应用这些配置。

首先定义配置：

```php
$config['displayErrorDetails'] = true;
$config['addContentLengthHeader'] = false;

$config['db']['host']   = 'localhost';
$config['db']['user']   = 'user';
$config['db']['pass']   = 'password';
$config['db']['dbname'] = 'exampleapp';
```

第一行很重要！开启它可以在开发环境中获取更多错误信息。第二行允许web服务器设置Content-Length头，可以让Slim行为更加可预测。

其他设置不是特定的keys/values，他们仅仅是我之后想要访问的一些数据。

现在把他们传入Slim，我们需要修改我们创建Slim/App对象的地方：

```php
$app = new \Slim\App(['settings' => $config]);
```

我们可以稍后从应用里访问到所有添加到$config数组里的设置。

## 为我们的类设置自动加载

Composer可以处理类的自动加载。进一步了解，请访问[使用Composer管理自动加载规则](https://getcomposer.org/doc/04-schema.md#autoload)。

我的设置很简单因为我只有很少的额外的类，他们在全局命名空间，文件在src/classes/目录里。所以为了自动加载他们，请在composer.json文件里添加autoload块：

```javascript
{
    "require": {
        "slim/slim": "^3.1",
        "slim/php-view": "^2.0",
        "monolog/monolog": "^1.17",
        "robmorgan/phinx": "^0.5.1"
    },
    "autoload": {
        "psr-4": {
            "": "classes/"
        }
    }
}
```

## 添加依赖

大多数应用都有依赖，Slim使用基于Pimple的DIC。这个例子使用Monolog和PDO连接MySQL。

依赖注入容器的思想是，你配置容器来加载应用需要的依赖，当应用需要他们的时候。一旦DIC创建/组装了这些依赖，它可以贮存他们，然后供以后需要的时候使用。

想要获取容器，我们可以在创建$app之后，注册路由之前，添加如下代码：

```php
$container = $app->getContainer();
```

现在我们有了Slim\Container对象，我们可以向里面添加服务。

### 使用Monolog

如果你已经熟悉Monolog，它是一个优秀了PHP日志框架，所以这里我们使用它。首先，通过Composer获取Monolog库：

```text
php composer.phar require monolog/monolog
```

将依赖命名为logger：

```php
$container['logger'] = function($c) {
    $logger = new \Monolog\Logger('my_logger');
    $file_handler = new \Monolog\Handler\StreamHandler('../logs/app.log');
    $logger->pushHandler($file_handler);
    return $logger;
};
```

我们向容器里添加了一个元素，它是一个匿名函数（传入的$c是container对象，所以你可以函数里访问其他的依赖）。当你第一访问这个依赖时，它会被调用；这里代码是对依赖的设置。下次我们想要访问同一个依赖时，直接使用第一次创建的对象。

我的Monolog配置很简单；仅仅设置了应用记录所有的错误到logs/app.log文件里（记住，这个路径是相对于脚本文件的，比如index.php）。

设置好了logger，我们可以在路由里这样使用它：

```php
$this->logger->addInfo('Something interesting happened');
```

记录日志是很好的习惯，所以我常建议这样做。它可以让你根据需要或多或少地添加debug日志，然后通过对每条信息使用相应的日志级别，你可以了解在每个时刻的详细信息。

### 添加数据库连接

对于PHP有很多的数据库类库，这里我们使用PDO - 它在PHP里作为标准，在每个项目里都可以用到，或者你可以通过调整下面的例子来使用自己的库。

和添加Monolog到DIC里一样，我们也添加一个匿名函数来建立以来，这里叫做db：

```text

```

