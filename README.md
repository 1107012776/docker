# docker
一些linux上面docker操作


### 命令

##### 进入容器
docker exec -it 54b43b9ed0b7 /bin/bash


##### 镜像构建
docker build -t nginx:v1 ./


##### 搜索镜像

$ docker search 镜像名称

例如：docker search mysql

##### 下载镜像

$ docker pull 镜像名

3. 查看宿主机上的镜像

$ docker images

##### 删除镜像

$ docker rmi 镜像ID/标签

##### 启动、停止、重启容器命令

$ docker start 容器ID|name|name:tag
$ docker stop 容器ID|name|name:tag
$ docker restart 容器ID|name|name:tag
容器ID=id name=容器名字 name:tag=容器:版本号

##### 查看当前运行的容器

$ docker ps

##### 查看所有容器

$ docker ps -a

##### 删除容器

$ docker rm 容器ID

##### 创建容器(重点)

$ docker create -it centos:latest
$ docker create -it --name tomcat01 centos:latest

##### 启动容器(重点)

$ docker exec -it 容器ID/容器NAME /bin/bash
##### 简写
$ docker exec -it 容器ID/容器NAME bash

##### 创建\启动\进入容器

$ docker run -it centos:latest /bin/bash

##### 指定了端口号
$ docker run -it -p 7001:8001 centos:latest /bin/bash

##### 使用 -P 标记时，Docker 会随机映射一个 49000~49900 的端口
$ docker run -it -P --name tomcat03 centos:latest /bin/bash

##### 开启端口号 firewall-cmd --zone=public --add-port=5671/tcp --permanent

firewall-cmd --zone=public --add-port=15671/tcp --permanent

##### 重启防火墙(不重启以上的设置是不会生效的)： firewall-cmd --reload
