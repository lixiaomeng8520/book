# 基础知识

## 中国镜像

### 源站

1. [阿里巴巴](https://opsx.alibaba.com/mirror)
2. [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/)
3. [科大开源镜像站](http://mirrors.ustc.edu.cn/)

### centos7 repo文件

{% tabs %}
{% tab title="centos" %}
```bash
[base]
name=centos - base
baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos/$releasever/os/$basearch/
enable=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-7

#released updates
[updates]
name=centos - updates
baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos/$releasever/updates/$basearch/
enable=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
name=centos - extras
baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos/$releasever/extras/$basearch/
enable=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-7
```
{% endtab %}

{% tab title="epel" %}
```bash
[epel]
name=epel
baseurl=https://mirrors.tuna.tsinghua.edu.cn/epel/7/$basearch
enabled=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/epel/RPM-GPG-KEY-EPEL-7
```
{% endtab %}

{% tab title="ius" %}
```bash
[ius - stable]
name=ius - stable
baseurl=https://mirrors.tuna.tsinghua.edu.cn/ius/stable/CentOS/7/$basearch
enabled=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/ius/IUS-COMMUNITY-GPG-KEY
```
{% endtab %}
{% endtabs %}

## 文件类型

| 字符 | 描述 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | 普通文件 |
| d | 目录 |
| c | 字符设备文件 |
| b | 块设备文件 |
| s | 接口文件 如我们开启MySQL服务后，在/var/lib/mysql/下生成的mysql.sock文件，关闭MySQL服务后，这个文件就消失了。 |
| p | 管道 |
| l | 符号链接文件 |



