# iptables

## 参考

* [linux平台下防火墙iptables原理\(转\)](http://www.cnblogs.com/ggjucheng/archive/2012/08/19/2646466.html)
* [25个iptables常用示例](https://www.cnblogs.com/bill1015/p/6847841.html)

## netfilter

linux内核通过netfilter模块实现网络访问控制功能，在用户层可以通过iptables程序对netfilter进行管理。

netfilter可以对数据包进行允许、丢弃、修改操作。

netfilter通过以下方式对数据包进行分类：

{% hint style="info" %}

* 源IP地址
* 目标IP地址
* 使用接口
* 使用协议（TCP、UDP、ICMP等）
* 端口号
* 连接状态（new、ESTABLISHED、RELATED、INVALID）

## 数据包流向

![](../.gitbook/assets/qq-jie-tu-20180507160859.png)

![](../.gitbook/assets/2012081915413532.png)

## 表和链

### filter

用以对数据进行过滤。

链：`INPUT`、`FORWARD`、`OUTPUT`

| **描述** | **命令** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 默认策略 | `iptables -P INPUT DROP` |
|  | `iptables -P FORWARD DROP` |
|  | `iptables -P OUTPUT DROP` |
| 控制INPUT和OUTPUT本机的网络流量 | `iptables -A INPUT -s 192.168.1.100 -j DROP` |
|  | `iptables -A INPUT -p tcp --dport 80 -j DROP` |
|  | `iptables -A INPUT -s 192.168.1.0/24 -p tcp --dport 22 -j DROP` |
|  | `iptables -A INPUT -i eth0 -j ACCEPT` |
|  | `iptables -A INPUT -m state --state ESTABLISHED -j ACCEPT` |
| 禁止 192.168.1.0/24 到 10.1.1.0/24 的流量 | `iptables -A FORWARD -s 192.168.1.0/24 -d 10.1.1.0/24 -j DROP` |

### nat

用以对数据包的源、目标地址进行修改。

* SNAT 源地址转换，用于伪装内部地址。
* DNAT 目标地址换砖，通常用于跳转。

链：`PREROUTING`、`OUTPUT`、`POSTROUTING`

| **描述** | **命令** |
| --- | --- | --- | --- | --- |
| 进入本机之前跳转 | `iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-dest 192.168.1.10` |
| 出本机之前跳转 | `iptables -t nat -A OUTPUT -p tcp --dport -j DNAT --to-dest 192.168.1.100:8080` |
| 伪装，一般意义的NAT，所有从 eth0 出的流量进行地址转换。因为公网地址经常是变化的，所以这里用 MASQUERADE | `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE` |
| 隐藏源地址 | `iptables -t nat -A POSTROUTING -j SNAT --to-source 1.2.3.4` |

### mangle

高级修改，TODO。

{% hint style="info" %}
链：PREROUTING、INPUT、FORWARD、OUTPUT、POSTROUTING
{% endhint %}

