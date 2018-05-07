# git

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



