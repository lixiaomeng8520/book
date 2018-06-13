# Supervisor

## 参考

* [官方](http://www.supervisord.org)

## 介绍

### 概览

* 方便：不用使用rc.d脚本。
* 精准：将进程作为子进程，精准获取信息。
* 代理：提供简单shell或web ui。
* 进程组：统一管理。

### 特性

* 简单：使用ini形式的配置文件。
* 集中式：使用统一方式管理，并提供命令行和web接口。
* 高效：通过fork/exec启动子进程，不用守护进程。
* 扩展：提供简单事件通知协议来监控它。
* 兼容：除了windows。
* 健壮：使用多年了。

### 组件

* supervisord：服务端。
* supervisorctl：客户端命令行。
* Web Server：web端控制，功能同supervisorctl。
* XML-RPC接口：接口。

### 需求

* unix like
* python &gt;= 2.4 &lt; 3

## 安装

### 联网安装

#### 使用Setuptools

```text
easy_install supervisor
```

#### 不使用Setuptools

* 下载软件包
* 解压软件包
* 执行 `python setup.py install`

### 离线安装

### 安装发行版包

```text
yum install supervisor
```

### 通过pip安装

```text
pip install supervisor
```

### 创建配置文件

```text
echo_supervisord_conf > /etc/supervisord.conf

echo supervisord_conf > supervisord.conf
supervisord -c supervisord.conf
```

## 运行

## 配置文件

## 子进程

## 日志

## 事件

