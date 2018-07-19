# docker

## 参考

* [概念](https://docs.docker.com/get-started/)
* [安装](https://docs.docker.com/install/linux/docker-ce/centos/)
* [dockerd 官方文档](https://docs.docker.com/engine/reference/commandline/dockerd/)
* [swarm 官方文档](https://docs.docker.com/engine/swarm/)
* [compose 官方文档](https://docs.docker.com/compose/overview/)
* [Dockerfile 最佳实战](https://docs.docker.com/v17.09/engine/userguide/eng-image/dockerfile_best-practices/)
* [官方商店](https://store.docker.com/)
* [跟我一起学Docker——RUN、ENTRYPOINT与CMD](https://www.binss.me/blog/learn-docker-with-me-about-run-entrypoint-and-cmd/)
* [Using GlusterFS with Docker swarm cluster](http://embaby.com/blog/using-glusterfs-docker-swarm-cluster/)

## 国内源

```javascript
{
    "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

## swarm

routing mess网络，访问任意一个节点，会自动分发到某一个task上，即使该节点没有task。

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 初始化swarm，并指定manager ip | `docker swarm init --advertise-addr 192.168.56.20` |
| 获取worker的join-token | `docker swarm join-token worker` |
| 加入集群 | `docker swarm join --token aaa 192.168.56.20` |
| 查看节点 | `docker node ls` |
| 部署一个服务 | `docker service create --replicas 1 --name helloworld alpine ping docker.com` |
| 查看服务 | `docker service ls` |
| 查看服务详情 | `docker service inspect --pretty helloworld` |
| 查看哪些节点在运行服务 | `docker service ps helloworld` |
| 伸缩服务 | `docker service scale hellowrld=5` |
| 删除服务 | `docker service rm helloworld` |
| 升级服务 | `docker service update --image redis:3.0.7 redis` |
| 剔除一个节点 | `docker node update --availability drain worker1` |
| 激活一个节点 | `docker node update --availability active worker1` |

## 网络

| 描述 | 命令 |
| --- | --- | --- | --- | --- |
| 列出所有网络 | `docker network ls` |
| 默认创建bridge网络 | `docker network create mybridge` |
| 查看mybridge网络详情 | `docker network inspect mybridge` |
| 指定容器的网络 | `docker run --network mybridge` |

## 卷

| 描述 | 命令 |
| --- | --- | --- | --- | --- | --- |
| 列出所有卷 | `docker volume ls` |
| 创建卷 | `docker volume create jenkins` |
| 删除卷 | `docker volume rm jenkins` |
| 查看卷详情 | `docker volume inspect jenkins` |
| 指定容器卷 | `docker run -v jenkins:/path/to` |

## TLS

