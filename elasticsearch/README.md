# docker安装elasticsearch


```bash
#!/bin/bash

#安装blog https://blog.csdn.net/qq_40942490/article/details/111594267

sysctl -w vm.max_map_count=262144
#拉取镜像
docker pull elasticsearch:7.7.0

#启动镜像
docker run --name elasticsearch -d -e ES_JAVA_OPTS="-Xms512m -Xmx512m" -e "discovery.type=single-node" -p 9200:9200 -p 9300:9300 elasticsearch:7.7.0

```
### 参数说明

--name表示镜像启动后的容器名称  

-d: 后台运行容器，并返回容器ID；

-e: 指定容器内的环境变量

-p: 指定端口映射，格式为：主机(宿主)端口:容器端口

### 查看
curl localhost:9200
```json
{
  "name" : "54b43b9ed0b7",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "6DaSbY0mSy-krJTvvcIHIw",
  "version" : {
    "number" : "7.7.0",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "81a1e9eda8e6183f5237786246f6dced26a10eaf",
    "build_date" : "2020-05-12T02:01:37.602180Z",
    "build_snapshot" : false,
    "lucene_version" : "8.5.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

# 安装elasticsearch-head
```hash
#!/bin/bash

#拉取镜像
docker pull mobz/elasticsearch-head:5

#创建容器
docker create --name elasticsearch-head -p 9100:9100 mobz/elasticsearch-head:5

#启动容器
docker start elasticsearch-head
```


# 教程


https://www.cnblogs.com/wish5714/p/13045879.html
#### 新建一个 Index

```bash
curl -X PUT "localhost:9200/customer/_doc/1?pretty" -H 'Content-Type: application/json' -d'
{
  "name": "John Doe"
}
'
```


#### 查询
```bash
curl -X GET "localhost:9200/customer/_search?pretty" -H 'Content-Type: application/json' -d'
{
    "query": {
        "bool": {
            "must": [
               {"match_phrase": { "name": "John Doe" } }
            ]
        }
    }
 }
 '
```

#### 分词
 https://github.com/1107012776/elasticsearch-analysis-ik 分词操作
 
##### 安装中文分词插件
https://github.com/medcl/elasticsearch-analysis-ik/
```bash
elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.7.0/elasticsearch-analysis-ik-7.7.0.zip
```
