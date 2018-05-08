# systemd

## 参考

1. [Systemd 入门教程：命令篇](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)

## 几个主命令

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- | --- |
| 管理服务 | systemctl |
| 启动耗时 | systemd-analyze |
| 主机信息 | hostnamectl |
| 本地化设置 | localectl |
| 时间设置 | timedatectl |
| 登录用户 | loginctl |

## 电源

| 描述 | 命令 |
| --- | --- | --- |
|  关机 | systemctl poweroff |
| 重启 | systemctl reboot |

## 系统资源

systemd 可以管理所有系统资源，不同的资源统称为 unit 。

| 描述 | 类型 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 系统服务 | Service |
| 多个unit构成一个组 | Target |
| 硬件设备 | Device |
| 文件系统挂载点 | Mount |
| 自动挂载点 | Automount |
| 文件或路径 | Path |
| 不是又systemd启动的外部进程 | Scope |
| 进程组 | Slice |
| systemd 快照 | Snapshot |
| 进程间通信的socket | Socket |
| swap文件 | Swap |
| 定时器 | Timer |



