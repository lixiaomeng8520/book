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

可以通过http://localhost:8080来访问应用（如果你本机已经使用了8080端口，会被警告。只需要换一个不同的端口即可，PHP并不关心具体绑定到哪里）。

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

注意：

