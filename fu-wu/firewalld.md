# firewalld

## 参考

* [How to Configure ‘FirewallD’ in RHEL/CentOS 7 and Fedora 21](https://www.tecmint.com/configure-firewalld-in-centos-7/)
* [Useful ‘FirewallD’ Rules to Configure and Manage Firewall in Linux](https://www.tecmint.com/firewalld-rules-for-centos-7/)

## 说明

* firewalld代替iptables.
* 两者不要同时存在.
* iptables使用INPUT, OUTPUT, FORWARD链; 但是firewalld使用Zones\(区域\)的概念.
* firewalld优势之一, 它预定义了一些服务.

Zone

| **名称** | **描述** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Drop Zone | 只出不进; 相当于iptables -j drop |
| Block Zone | 禁止进入, 通过icmp-host-prohibited拒绝, 只允许本机内建立的连接. |
| Public Zone | 允许特定的端口 |
| External Zone | TODO: nat |
| DMZ Zone |  |
| Work Zone |  |
| Home Zone |  |
| Internal Zone |  |
| Trusted Zone |  |

## 命令

| **描述** | **命令** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 状态 | `firewall-cmd --state` |
| 重载配置 | `firewall-cmd --reload` |
|  |  |
| 获取所有zone | `firewall-cmd --get-zones` |
| 获取默认zone | `firewall-cmd --get-default-zone` |
| 获取public zone详细信息 | `firewall-cmd --list-all --zone=public` |
| 设置默认zone | `firewall-cmd --set-default-zone=drop` |
|  |  |
| 获取所有服务 | `firewall-cmd --get-services` |
| 列出系统自带服务 | `ls /usr/lib/firewalld/services` |
|  |  |
| public zone添加服务 | `firewall-cmd --zone=public --add-service=http --permanent` |
| 添加8001端口 | `firewall-cmd --zone=public --add-port=8001/tcp --permanent` |

## 服务配置

### 配置文件路径

| **描述** | **路径** |
| --- | --- | --- |
| 系统 | `/usr/lib/firewalld/services` |
| 自定义 | `/etc/firewalld/services` |

### 添加自定义服务

拷贝一份系统配置文件到自定义配置路径

```bash
cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/rtmp.xml
```

修改标题、描述、协议、端口

```markup
<?xml version="1.0" encoding="utf-8"?>
<service>
    <short>rtmp</short>
    <description>rtmp</description>
    <port protocol="tcp" port="1953" />
</service>
```

