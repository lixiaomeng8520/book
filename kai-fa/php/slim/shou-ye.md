# 首页

## 欢迎

Slim是一个小型的PHP框架，它可以帮助你快速写出简单却又强大的web应用程序和API。本质上，Slim是一个接收HTTP请求的分发器，调用相应的回调例程，最后返回一个HTTP响应。

## 关键点

Slim是一个理想的工具来创建API，用于处理，重新调整用途或发布数据。Slim也是一个快速创建原型的很好的工具。但是，你也甚至可以构建包含用户界面的完整功能的web应用。更重要的是，Slim非常快，它只有很少的代码。实际上，你可以用一下午时间来读完它的源码。

> 本质上，Slim是一个接收HTTP请求的分发器，调用相应的回调例程，最后返回一个HTTP响应。

你不用总是需要一个像Symfony或Lavarel一样功能非常齐全的解决方案。确实它们很不错。但是它们经常矫枉过正。相反，Slim只提供一个很小的工具集来完成你的需求

## 工作原理

首先，你需要一个web服务器，比如Nginx或Apache。你应该配置你的web服务器，以便他们可以发送所有合适的请求到一个PHP文件。在这个文件里，你实例化和运行你的Slim程序。

一个Slim程序包含一批响应特定HTTP请求的路由。每个路由触发一个回调，然后返回一个HTTP响应。第一步，初始化和配置Slim应用；然后，定义路由；最后，运行应用。下面是个例子：

```php
<?php
// Create and configure Slim app
$config = ['settings' => [
    'addContentLengthHeader' => false,
]];
$app = new \Slim\App($config);

// Define app routes
$app->get('/hello/{name}', function ($request, $response, $args) {
    return $response->write("Hello " . $args['name']);
});

// Run app
$app->run();
```

## 请求和响应

当你要构建Slim应用，你要经常面对Request和Response对象。这些对象代表从web服务器接收的实际的HTTP请求，和最终返回个客户端的HTTP响应。

每个Slim应用路由都将当前的Request和Response对象作为回调例程的参数。这些对象实现了流行的[PSR-7](https://www.slimframework.com/docs/v3/concepts/value-objects.html)接口。Slim应用路由可以根据需要检查或操作这些对象。最终，每个路由必须返回实现了PSR-7的Response对象。

## 自定义组件

Slim可以和其他PHP组件很好的配合工作。你可以注册第三方的组件，比如基于Slim默认功能构建的Slim-Csrf, Slim-HttpCache, 或Slim-Flash。它也可以很容易和[Packagist](https://packagist.org/)上的第三方组件集成。

## 如何阅读本文档

如果你是新手，我建议你重头到尾阅读。如果你已经很熟悉Slim了，可以直接跳到相应的章节。

本文档从介绍Slim的概念和架构开始，然后是特定的章节，比如请求和响应处理，路由，和错误处理。

