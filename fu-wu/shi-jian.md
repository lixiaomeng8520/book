# 时间

## timedatectl

使用 timedatectl 来统一管理时间，他是systemd的一部分，如果设置 ntp 同步，他会调用 ntp 或 chrony 来进行同步

```bash
# 当前时间状态
timedatectl status
```

## chrony 配置

修改 /etc/chrony.conf 配置文件

```bash
# 修改 server
server 0.cn.pool.ntp.org iburst
server 1.cn.pool.ntp.org iburst
server 2.cn.pool.ntp.org iburst
server 3.cn.pool.ntp.org iburst
```

重启

```bash
systemctl restart chronyd
```

