# git

## 教程

[https://git-scm.com/book/zh/v2](https://git-scm.com/book/zh/v2)

## ss代理ssh

ss右键 -&gt; 允许来自局域网的连接。

安装connect-proxy

```bash
yum -y install connect-proxy
```

编辑 ~/.ssh/config 文件

```bash
# ~/.ssh/config

Host github.com *.github.com
    ProxyCommand connect-proxy -H 192.168.56.1:1080 %h %p
    IdentityFile ~/.ssh/id_rsa
    User git
```

## 安装

```bash
# ius
yum install git2u
```

## 配置

### 配置文件

| 命令 | 路径 | 描述 |
| --- | --- | --- | --- |
| git config | 当前项目目录 | 项目配置，作用于当前项目 |
| git config --global | ~/.gitconfig | 家目录，作用于当前用户 |
| git config --system | /etc/gitconfig | 全局配置 |

{% hint style="info" %}
git config \[--global\|--system\] -e  打开对应配置文件进行编辑
{% endhint %}

### 常用配置

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- | --- |
| 设置用户名 | git config user.name lixiaomeng |
| 设置邮箱 | git config user.email lixiaomeng8520@163.com |
| 忽略文件权限 | git config core.filemode false |
| 提交转换lf，检出不转换 | git config core.autocrlf input |
| 提交转换lf，检出转换crlf | git config core.autocrlf true |
| 提交检出均不转换 | git config core.autocrlf false |

## 工作流

![](../.gitbook/assets/git-model-2x.png)

## 命令

