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
cat > /etc/yum.repos.d/centos.repo <<EOF
[base]
name=CentOS-7 - Base
baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos/7/os/\$basearch/
#mirrorlist=http://mirrorlist.centos.org/?release=7&arch=\$basearch&repo=os
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-7

#released updates
[updates]
name=CentOS-7 - Updates
baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos/7/updates/\$basearch/
#mirrorlist=http://mirrorlist.centos.org/?release=7&arch=\$basearch&repo=updates
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
name=CentOS-7 - Extras
baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos/7/extras/\$basearch/
#mirrorlist=http://mirrorlist.centos.org/?release=7&arch=\$basearch&repo=extras
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-7
EOF
```
{% endtab %}

{% tab title="epel" %}
```bash
cat > /etc/yum.repos.d/epel.repo <<EOF
[epel]
name=epel
baseurl=https://mirrors.tuna.tsinghua.edu.cn/epel/7/\$basearch
enabled=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/epel/RPM-GPG-KEY-EPEL-7
EOF
```
{% endtab %}

{% tab title="ius" %}
```bash
cat > /etc/yum.repos.d/ius.repo <<EOF

[ius-stable]
name=ius - stable
baseurl=https://mirrors.tuna.tsinghua.edu.cn/ius/stable/CentOS/7/\$basearch
enabled=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/ius/IUS-COMMUNITY-GPG-KEY
EOF
```
{% endtab %}

{% tab title="docker" %}
```bash
cat > /etc/yum.repos.d/docker.repo <<EOF

[docker-ce-stable]
name=Docker CE Stable - \$basearch
baseurl=https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/centos/7/\$basearch/stable
enabled=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/centos/gpg
EOF
```
{% endtab %}

{% tab title="mongodb" %}
```bash
cat > /etc/yum.repos.d/mongodb.repo <<EOF
[mongodb-org]
name=MongoDB Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/mongodb/yum/el7/
gpgcheck=0
enabled=1
EOF
```
{% endtab %}
{% endtabs %}

## 文件类型

| 字符 | 描述 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `-` | 普通文件 |
| `d` | 目录 |
| `c` | 字符设备文件 |
| `b` | 块设备文件 |
| `s` | 接口文件 如我们开启MySQL服务后，在/var/lib/mysql/下生成的mysql.sock文件，关闭MySQL服务后，这个文件就消失了。 |
| `p` | 管道 |
| `l` | 符号链接文件 |





