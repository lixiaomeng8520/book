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

