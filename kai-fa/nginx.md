# nginx

## 参考

* [官方文档](http://nginx.org/en/docs/)
* [简明 Nginx Location Url 配置笔记](https://www.jianshu.com/p/e154c2ef002f)
* [FASTCGI\_PARAMS VERSUS FASTCGI.CONF – NGINX CONFIG HISTORY](https://blog.martinfjordvald.com/2013/04/nginx-config-history-fastcgi_params-versus-fastcgi-conf/)
* [How to Install Nginx on CentOS 7](https://www.tecmint.com/install-nginx-on-centos-7/)

## location 规则

### 语法

* location \[ = \| ~ \| ~\* \| ^~ \] uri { ... }
* location @name { ... }

### 匹配模式

|  优先级 |  模式 |  语法 |  区分大小写 |  使用正则 |  描述 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 |  精确匹配 |  location = /demo {} |  是 |  否 |  |
| 2 |  前缀匹配 |  location ^~ /demo {} |  是 |  否 |  静态文件夹 |
| 3 |  正则匹配 |  location ~ /demo {} |  是 |  是 |  |
| 3 |  正则匹配 |  location ~\* /demo {} |  否 |  是 |  |
| 4 |  正常匹配 |  location /demo {} |  否 |  是 |  |
| 5 |  全匹配 |  location / {} |  是 |  否 |  |

### 说明

首先遵循大的优先级。

同级别内：

1. 正则匹配成功之后停止匹配，非正则匹配成功还会接着匹配。
2. 在所有匹配成功的url中，选取匹配度最大的url字符地址。

## 变量

| 变量名 | 描述 |
| --- | --- | --- | --- | --- | --- |
| uri | 域名后 / 到第一个 ? 之前 |
| is\_args | 第一个 ? |
| args | 第一个 ? 之后的内容 |
| request\_uri | 域名后 / 到最后 |
| fastcgi\_script\_name | 目前看同 uri |

## 杂项

fastcgi.conf 比 fastcgi\_params 多了一行SCRIPT\_FILENAME，应该使用前者。

fastcgi\_split\_path\_info 会根据正则表达式重新赋值两个变量`fastcgi_script_name`和`fastcgi_path_info`, 如下示例：

```bash
location ~ ^(.+\.php)(.*)$ {
    fastcgi_split_path_info ^(.+\.php)(.*)$;
    fastcgi_param SCRIPT_FILENAME $fastcgi_script_name;
    fastcgi_param PATH_INFO $fastcgi_path_info;
}
```

## 优化



