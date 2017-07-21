# overview
## image container Repository
镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
按照 Docker 最佳实践的要求，容器不应该向其存储层内写入任何数据，容器存储层要保持无状态化。所有的文件写入操作，都应该使用 数据卷（Volume）、或者绑定宿主目录，在这些位置的读写会跳过容器存储层，直接对宿主(或网络存储)发生读写，其性能和稳定性更高。
一个 Docker Registry 中可以包含多个仓库（Repository）；每个仓库可以包含多个标签（Tag）；每个标签对应一个镜像。

## docker install 





# docker-machine
## ls
## create
docker-machine create --driver=virtualbox default
## env
docker-machine env default
docker-machine env default | Invoke-Expression
## ssh
docker-machine ssh default

# docker
## images
查看image
### -f
过滤器参数 --filter，简写-f
比如希望看到在 mongo:3.2 之后建立的镜像，可以用 images -f since=mongo:3.2 之前则用before
### -q
列出id
### format
docker images --format "{{.ID}}: {{.Repository}}"
docker images --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"

## rmi
删除镜像
docker rmi $(docker images -q -f dangling=true) 删除虚悬镜像

## docker ps 
查看哪些container
* –a



