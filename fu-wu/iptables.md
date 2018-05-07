# iptables

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
{% endhint %}

## 数据包流向

![](../.gitbook/assets/qq-jie-tu-20180507160859.png)

## 表和链

### filter

用以对数据进行过滤。

{% hint style="info" %}
链：INPUT、FORWARD、OUTPUT
{% endhint %}

```bash
# 控制INPUT和OUTPUT本机的网络流量
iptables -A INPUT -s 192.168.1.100 -j DROP
iptables -A INPUT -p tcp --dport 80 -j DROP
iptables -A INPUT -s 192.168.1.0/24 -p tcp --dport 22 -j DROP
iptables -A INPUT -i eth0 -j ACCEPT

# 当linux作为路由（进行数据转发）设备使用的时候，可以通过定义forward规则来进行转发控制
# 禁止 192.168.1.0/24 到 10.1.1.0/24 的流量
iptables -A FORWARD -s 192.168.1.0/24 -d 10.1.1.0/24 -j DROP
```

### nat

用以对数据包的源、目标地址进行修改。

* SNAT 源地址转换，用于伪装内部地址。
* DNAT 目标地址换砖，通常用于跳转。

{% hint style="info" %}
链：PREROUTING、OUTPUT、POSTROUTING
{% endhint %}

```bash
# 进入本机之前跳转
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-dest 192.168.1.10

# 出本机之前跳转
iptables -t nat -A OUTPUT -p tcp --dport -j DNAT --to-dest 192.168.1.100:8080

# 伪装，一般意义的NAT
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

# 隐藏源地址
iptables -t nat -A POSTROUTING -j SNAT --to-source 1.2.3.4
```

### mangle

高级修改，TODO。

{% hint style="info" %}
 链：PREROUTING、INPUT、FORWARD、OUTPUT、POSTROUTING
{% endhint %}



