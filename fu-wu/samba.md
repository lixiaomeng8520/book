# samba

## 安装

```bash
yum -y install samba
```

## 查看用户

```bash
pdbedit -L
```

## 添加用户，只能添加系统存在的用户

```bash
smbpasswd -a root
```

## 修改配置

```bash
# vim /etc/samba/smb.conf

[homes]
xxxx
valid users = root
xxxx
```

## 启动

```bash
systemctl start smb
systemctl enable smb
```

## 访问

在windows资源管理器里输入 \192.168.56.20\

