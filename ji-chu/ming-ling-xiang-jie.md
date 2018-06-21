# 命令详解

## 参考

1. [linux命令大全](http://www.runoob.com/linux/linux-command-manual.html)
2. [linux系统排查](https://www.cnblogs.com/Security-Darren/p/4685629.html)

## 2&gt;&1

希望将标准错误和标准输出都重定向到一个文件中，那么不要分别重定向，因为会打开文件两次，下面是将标准错误重定向到标准输出，再由标准输出重定向到文件。

```text
command > a.log 2>&1
```

## nmcli

nmcli - command-line tool for controlling NetworkManager

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 查看所有设备 | `nmcli d` |
| 查看所有连接 | `nmcli c` |
| 查看static这个连接 | `nmcli c show static` |
| 添加dhcp连接 | `nmcli c add con-name dhcp type ethernet ifname enp0s3` |
| 添加static连接 | `nmcli c add con-name static type ethernet ifname enp0s3 ip4 192.168.56.20/24 gw4 192.168.56.1` |
| 修改连接属性，参考show属性 | `nmcli c mod static ipv4.addresses 192.168.56.20/24` |
| 修改连接为静态连接 | `nmcli c mod static ipv4.method manual` |
| 启动static连接 | `nmcli c up static` |
| 关闭static连接 | `nmcli c down static` |

## netstat

netstat 是一款命令行工具，可用于列出系统上所有的网络套接字连接情况，包括 tcp, udp 以及 unix 套接字，另外它还能列出处于监听状态（即等待接入请求）的套接字。

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 列出所有 | `netstat -a` |
| 列出tcp | `netstat -at` |
| 列出udp | `netstat -au` |
| 禁用域名解析 | `netstat -ant` |
| **监听中的连接** | `netstat -ntl` |
| 获取进程名 | `netstat -ntlp` |
| 获取进程用户 | `netstat -ntlpe` |
| 获取内核路由 | `netstat -nr` |

## lrzsz

rz, sz便是Linux/Unix同Windows进行ZModem文件传输的命令行工具。

安装 `yum install lrzsz`

| 描述 | 命令 |
| --- | --- | --- |
| 从windows receive接收文件 | rz |
| 发送文件a.txt到windows | sz a.txt |

## curl

-L 跳转

| 描述 | 命令 |
| --- | --- | --- |
| 下载 | `curl -L url -o target` |
| POST请求 | `curl -X POST -H Content-Type:text/html url -d postdata` |

## ssh

| 描述 | 命令 |
| --- | --- | --- | --- |
| 生成密钥 | `ssh-keygen -t rsa` |
| 拷贝公钥 | `ssh-copy-id root@master` |
|  | `ssh-copy-id -i ~/.ssh/id_rsa.pub root@master` |

## rpm

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- |
| 查看一个包的依赖 | `yum deplist php71u-cli` |
| 查询php71u是否安装 | `rpm -q php71u-fpm` |
| 查看php71u包信息 | `rpm -qi php71u-fpm` |
| 列出php71u包含的文件 | `rpm -ql php71u-fpm` |
| 查看filename属于哪个rpm包 | `rpm -qf filename` |

## tar

压缩文件时，会保留指定文件的路径。

指定文件是相对于-C参数的，如果没有，则是当前目录。

| 描述 | 命令 |
| --- | --- | --- | --- | --- |
| 解压到当前文件夹 | `tar -zxvf xx.tar.gz` |
| 解压到指定文件夹 | `tar -zxvf xx.tar.gz -C dir` |
| 列出包文件 | `tar -ztvf xx.tar.gz` |
| 指定文件（夹）压缩 | `tar -zcvf xx.tar.gz a.txt b/` |
| 全部文件压缩 | `tar -zcvf xx.tar.gz .` |
| 指定目录下的文件压缩 | `tar -zcvf xx.tar.gz -C /data b/ a.txt` |

## wc

 利用wc指令我们可以计算文件的Byte数、字数、或是列数，若不指定文件名称、或是所给予的文件名为"-"，则wc指令会从标准输入设备读取数据。

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 统计文件信息 | `wc file` （行数，单词数，字节数） |
| 显示file文件行数 | `wc -l file` |
| 显示文件单词数 | `wc -w file` |
| 显示文件byte数 | `wc -c file` |
| 统计文件夹下普通文件个数 | `ls -l dir | grep '^-' | wc -l` |
| 统计文件夹下目录个数 | `ls -l dir | grep '^d' | wc -l` |
| 统计所有层级文件夹普通文件个数 | `ls -lR dir | grep '^-' | wc -l` |

## sed

 Linux sed命令是利用script来处理文本文件。

sed可依照script的指令，来处理、编辑文本文件。

Sed主要用来自动编辑一个或多个文件；简化对文件的反复操作；编写转换程序等。

| 描述 | 命令 |
| --- | --- |
| file文件全局替换 | `sed -i 's/原字符串/替换字符串/g' file` |

## scp

目标是目录的，则是将源文件（夹）复制到到该目录里。

目标不存在的，则源是目录，则新建目录；源是文件，则新建文件。

| 描述 | 命令 |
| --- | --- | --- | --- |
| 复制文件到目录 | `scp user@host:/remotefile /localdir/` |
| 复制文件到文件 | `scp user@host:/remotefile /localfile` |
| 复制目录 | `scp -r user@host:/remotedir/ /localdir/` |

## /etc/passwd 文件

/etc/passwd 文件存放的是用户的信息，由6个冒号组成的7个信息

| 栏目 | 描述 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 用户名 | 用于区分不同的用户。在同一系统中注册名是惟一的。在很多系统上，该字段被限制在8个字符\(字母或数字\)的长度之内；并且要注意，通常在Linux系统中对字母大小写是敏感的。这与MSDOS/Windows是不一样的。 |
| 密码 | 系统用口令来验证用户的合法性。超级用户root或某些高级用户可以使用系统命令passwd来更改系统中所有用户的口令，普通用户也可以在登录系统后使用passwd命令来更改自己的口令。现在的Unix/Linux系统中，口令不再直接保存在passwd文件中，通常将passwd文件中的口令字段使用一个“x”来代替，将/etc /shadow作为真正的口令文件，用于保存包括个人口令在内的数据。当然shadow文件是不能被普通用户读取的，只有超级用户才有权读取。 |
| UID | UID是一个数值，是Linux系统中惟一的用户标识，用于区别不同的用户。在系统内部管理进程和文件保护时使用 UID字段。在Linux系统中，注册名和UID都可以用于标识用户，只不过对于系统来说UID更为重要；而对于用户来说注册名使用起来更方便。在某些特 定目的下，系统中可以存在多个拥有不同注册名、但UID相同的用户，事实上，这些使用不同注册名的用户实际上是同一个用户。 |
| GID | 这是当前用户的缺省工作组标识。具有相似属性的多个用户可以被分配到同一个组内，每个组都有自己的组名，且以自己的组标 识号相区分。像UID一样，用户的组标识号也存放在passwd文件中。在现代的Unix/Linux中，每个用户可以同时属于多个组。除了在 passwd文件中指定其归属的基本组之外，还在/etc/group文件中指明一个组所包含用户。 |
| 描述 | 包含有关用户的一些信息，如用户的真实姓名、办公室地址、联系电话等。在Linux系统中，mail和finger等程序利用这些信息来标识系统的用户。 |
| 家目录 | 该字段定义了个人用户的主目录，当用户登录后，他的Shell将把该目录作为用户的工作目录。 在Unix/Linux系统中，超级用户root的工作目录为/root；而其它个人用户在/home目录下均有自己独立的工作环境，系统在该目录下为每 个用户配置了自己的主目录。个人用户的文件都放置在各自的主目录下。 |
| Shell | 就是对登录命令进行解析的工具，Shell是当用户登录系统时运行的程序名称，通常是一个Shell程序的全路径名， 如/bin/bash\(若为空格则缺省为/bin/sh\)。 |

