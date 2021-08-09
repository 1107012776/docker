# docker
一些linux上面docker操作


### 命令

##### 进入容器
docker exec -it 54b43b9ed0b7 /bin/bash


##### 镜像构建
docker build -t nginx:v1 ./