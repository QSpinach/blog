---
tags: [Docker]
comments: true
toc: true
---



### docker安装

```
$ sudo yum remove docker \docker-client \ 
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
$ sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
$ sudo yum makecache fast
$ sudo yum -y install docker-ce
$ sudo systemctl start docker
```

### Dockerfile 

```dockerfile
FROM docker-registry.xxx/docker/nginx:1.13.6
COPY ./dist /var/www/html
COPY ./custom.conf /etc/nginx/conf.d/ 
RUN rm /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx","-g","daemon off;"]
```



### build镜像
```
docker build -t 镜像名 .
```

### 运行容器
```sh
docker run -it --name 容器名 -p 80:80 镜像id
```

### 查看日志

```bash
docker logs -f -t --since=“2017-05-31” --tail=10 容器
–since : 此参数指定了输出日志开始日期，即只输出指定日期之后的日志。
-f : 查看实时日志
-t : 查看日志产生的日期
-tail=10 : 查看最后的10条日志。
```

### 几个命令

```bash
docker start/stop/restart 容器id #启动暂停重启
docker rm 容器id #删除
docker kill 容器id #杀掉一个运行中的容器。
docker pause/unpause 容器id #暂停/取消暂停
docker create 镜像 // 创建容器但是不运行
docker exec -i -t 容器 /bin/bash #开启一个交互模式的终端
docker rmi <image id> # 移除镜像
docker rmi $(docker images | grep "none" | awk '{print $3}') #移除为none的镜像
docker rm $(docker ps -a | grep "Exited" | awk '{print $1 }') #移除为exited的容器
docker images -a 查看镜像
docker ps -a 查看容器
```