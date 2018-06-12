## 部署

恭喜！阅读到这里，你已经可成功使用Slim构建一些美妙的东西了。但是，还不到庆祝的时候。我们必须将我们的应用推到生产服务器上。

除了本文档之外，还有很多方式来部署。本章节，我们提供一些设置。

### 生产环境禁用错误输出

首先调整你的设置（在例子的src/settings.php文件），保证你不会对外输出错误。

```php
'displayErrorDetails' => false, // set to false in production
```

确保php.ini文件里也不会输出错误：

```
display_errors = 0
```

### 部署到你自己的服务器

如果你可以控制你的服务器，你应该使用下面的部署系统来建立一个部署程序：

* Deploybot
* Capistrano
* Script controlled with Phing, Make, Ant等

查看Web服务器文档来配置你的web服务器。

### 部署到共享的服务器

如果你的共享服务器运行Apache，你需要创建一个.htaccess文件在你的web服务器根目录（经常是htdocs，public，public_html或www），包含下面的代码：

```
<IfModule mod_rewrite.c>
   RewriteEngine on
   RewriteRule ^$ public/     [L]
   RewriteRule (.*) public/$1 [L]
</IfModule>
```

（将‘public’替换为你域名的正确名字，比如example.com/$1）

现在上传所有文件。由于你使用共享主机，可以通过FTP完成，你可以使用任何FTP客户端，比如Filezilla。
