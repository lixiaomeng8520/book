# git

## 教程

* 官方教程
* [易百git教程](https://www.yiibai.com/git/)
* [git的reset和checkout的区别](https://segmentfault.com/a/1190000006185954)

## 安装

```bash
# ius
yum install git2u
```

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

## 配置

### 配置文件

{% hint style="info" %}
git config \[--global\|--system\] -e  打开对应配置文件进行编辑
{% endhint %}

| 命令 | 路径 | 描述 |
| --- | --- | --- | --- |
| git config | 当前项目目录 | 项目配置，作用于当前项目 |
| git config --global | ~/.gitconfig | 家目录，作用于当前用户 |
| git config --system | /etc/gitconfig | 全局配置 |

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

### branch

> 可以有多个远程仓库，本地分支可以设置不同仓库的远程分支。
>
> 本地分支的跟踪分支只有一个。

### pull

> 没有写本地分支的，都是指当前分支。
>
> 没有写远程分支的，则必须当前分支有跟踪的远程分支，否则会报错。

| 描述 | 命令 |
| --- | --- | --- | --- | --- |
| 完整形式 | git pull server remote\_branch:local\_branch |
| 与当前分支合并 | git pull server remote\_branch |
| 与当前分支合并（从**跟踪分支**） | git pull server |
| 与当前分支合并（从**跟踪分支**） | git pull |

### push

> 推送原则上要同名

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- |
| 完整形式 | git push server local\_branch:remote\_branch |
| 推送到同名分支，不存在则新建 | git push server local\_branch |
| 当前分支要和**跟踪分支**同名 | git push server |
| 当前分支要和**跟踪分支**同名 | git push |
| 删除远程分支 | git push server :remote\_branch |



