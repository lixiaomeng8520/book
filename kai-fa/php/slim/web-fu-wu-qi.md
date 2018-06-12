# Web服务器

通常使用前端控制器模式将从web服务器接收的相应的HTTP请求集中到一个PHP文件里。下面介绍如何告诉web服务器将HTTP请求发送到你的PHP前端控制器文件。

## PHP内置服务器

执行下面的命令启动本地服务器，假设 ./public/ 是可访问的目录，里面有 index.php 文件：

```text
php -S localhost:8888 -t public public/index.php
```

## Apache配置

确定你的 .htaccess 文件和 index.php 文件在同一个可访问目录下。.htaccess 文件内容：

```text
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.php [QSA,L]
```

.htaccess 文件需要URL重写。保证Apache的mod\_rewrite模块开启，并且虚拟主机里看配置了AllowOverride 选项，以便.htaccess 的重写规则生效：

```text
AllowOverride All
```

## Nginx配置

这是为域名example 配置的Nginx虚拟主机例子。它监听在80端口，并且假设PHP-FPM运行在9000端口上。请根据实际情况修改server\_name ，error\_log ，access\_log 和root 指令。root 指令表示应用程序的根目录；你的Slim应用的index.php 文件在这个目录里：

```text
server {
    listen 80;
    server_name example.com;
    index index.php;
    error_log /path/to/example.error.log;
    access_log /path/to/example.access.log;
    root /path/to/public;
​
    location / {
        try_files $uri /index.php$is_args$args;
    }
​
    location ~ \.php {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param SCRIPT_NAME $fastcgi_script_name;
        fastcgi_index index.php;
        fastcgi_pass 127.0.0.1:9000;
    }
}
```

## HipHop虚拟主机

HipHop虚拟主机配置应该包含下面的代码。保证修改SourceRoot指向你的Slim应用跟目录。

```text
Server {
    SourceRoot = /path/to/public/directory
}
​
ServerVariables {
    SCRIPT_NAME = /index.php
}
​
VirtualHost {
    * {
        Pattern = .*
        RewriteRules {
                * {
                        pattern = ^(.*)$
                        to = index.php/$1
                        qsa = true
                }
        }
    }
}
```

## IIS

保证Web.config文件和index.php文件在同一个可访问的目录。Web.config目录应该包含下面的代码：

```text
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <rewrite>
            <rules>
                <rule name="slim" patternSyntax="Wildcard">
                    <match url="*" />
                    <conditions>
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="index.php" />
                </rule>
            </rules>
        </rewrite>
    </system.webServer>
</configuration>
```

## lighttpd

你的lighttpd配置文件应该包含下面的代码。需要lighttpd&gt;=1.4.24。

```text
url.rewrite-if-not-file = ("(.*)" => "/index.php/$0")
```

假设Slim应用的index.php文件在你项目的根目录（www root）。

