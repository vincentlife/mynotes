# overview
## image container Repository
镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
按照 Docker 最佳实践的要求，容器不应该向其存储层内写入任何数据，容器存储层要保持无状态化。所有的文件写入操作，都应该使用 数据卷（Volume）、或者绑定宿主目录，在这些位置的读写会跳过容器存储层，直接对宿主(或网络存储)发生读写，其性能和稳定性更高。
一个 Docker Registry 中可以包含多个仓库（Repository）；每个仓库可以包含多个标签（Tag）；每个标签对应一个镜像。

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
* -f
过滤器参数 --filter，简写-f
比如希望看到在 mongo:3.2 之后建立的镜像，可以用 images -f since=mongo:3.2 之前则用before
* -q 列出id
* format docker images --format "{{.ID}}: {{.Repository}}"
docker images --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"

## rmi rm
删除镜像
docker rmi $(docker images -q -f dangling=true) 删除虚悬镜像
删除容器
-f, --force     Force the removal of a running container (uses SIGKILL)
  --help      Print usage
-l, --link      Remove the specified link
-v, --volumes   Remove the volumes associated with the container

## ps 
* –a 查看所有container

## run
* --name 指定容器名，
* -t 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上
* -i 让容器的标准输入保持打开。
* --restart
=always：无论容器的退出代码是什么，Docker都会自动重启该容器。
=on-failure：只有当容器的退出代码为非0值的时候才会自动重启。
* -d 把启动的Container放在后台运行。-d=true
* -e 设置环境变量

### docker run demo
* docker run ubuntu:14.04 /bin/echo 'Hello world'
输出一个 “Hello World”，之后终止容器。
* docker run --name my_container -it ubuntu:14.04 /bin/bash

## start restart
start 启动一个已停止的容器
* -a attach，绑定stdout,stderr
* -i 绑定stdin

## stop kill
用docker stop命令来停掉容器的时候，docker默认会允许容器中的应用程序有10秒的时间用以终止运行。
docker kill --signal=SIGINT container_name
与docker stop命令不一样的地方在于，docker kill没有任何的超时时间设置，它会直接发送SIGKILL信号，以及用户通过signal参数指定的其他信号。

## diff inspect logs
* diff会列出3种容器内文件状态变化（A - Add, D - Delete, C - Change ）的列表清单。构建Image的过程中需要的调试指令。
* inspect 查看容器或镜像的信息
* logs 查看容器运行的log


# dockerfile
## build
根据dockerfiles构建镜像

      --no-cache=false Do not use cache when building the image  
      -q, --quiet=false Suppress the verbose output generated by the containers  
      --rm=true Remove intermediate containers after a successful build  
      -t, --tag="" Repository name (and optionally a tag) to be applied to the resulting image in case of success  
$docker build -t image_name Dockerfile_path







