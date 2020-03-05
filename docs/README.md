# 系统整体架构

![系统整体架构图](https://github.com/MarkShen1992/docker-kubernetes-practice/blob/master/docs/archetecture.png)

# 容器的 Endpoint 配置

| 服务名称            | IP地址        | 端口号 |
| :------------------ | :------------ | :----- |
| user-service        | 192.168.1.102 | 7911   |
| user-edge-service   | 192.168.1.102 | 8082   |
| message-service     | 192.168.1.102 | 9090   |
| course-service      | 192.168.1.102 | 8081   |
| course-edge-service | 192.168.1.102 | 8083   |
| api-gateway-zuul    | 192.168.1.102 | 8080   |
| mysql               | 192.168.1.102 | 3307   |
| zookeeper           | 192.168.1.102 | 2181   |
| redis               | 192.168.1.102 | 6379   |

# Docker 容器部署应用程序

## Docker 容器间通讯方案

- 通过容器的 Endpoint 去做
- 服务把端口映射出去，容器端口转换成主机端口 
  - zk, redis, mysql
- 使用Docker link地址的方式，然后通过名字就可以实现 Docker 容器之间的通信了 
  - api-gateway-zuul, message-service etc

### 使用 Docker 的 docker-compose 来实现

使用 `docker compose`去描述服务之间的关系非常好用，当然也可以使用 Docker 命令去建立 link 关系

在使用[Docker compose](https://github.com/docker/compose/releases)前要对其进行安装

```
curl -L https://github.com/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

编写 `docker-compose.yml`文件，文件见程序中 [micro-service](https://github.com/MarkShen1992/docker-kubernetes-practice/tree/master/micro-service)

docker-compose 使用命令

```
docker-compose up -d --启动服务
docker-compose down -d --关闭服务
docker-compose up -d service-name --单独启动某个服务
```

使用Portainer来管理Docker，查看[Portainer安装](https://markshen1992.github.io/document/devops/ops/linux/docker_visualize.html)来安装Portainer `Docker 管理工具`。

**Note:** 使用 docker-compose up -d 来启动所有容器的时候，开启程序对应的端口号

- [Linux环境下开启端口号命令](https://markshen1992.github.io/document/devops/ops/linux/linux_basic_command.html)
