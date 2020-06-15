# Docker  (What、Why 和 How )

## 是什么 能干什么

Build Once, Run Anywhere
容器是一种轻量级的，可移植的，自包含的软件打包技术，使应用程序可以在几乎任何地方以相同的方式运行。
**环境无关性** **动态扩容**

## 和虚拟机对比

隔离程度不同
容器依赖于用户空间。 虚拟机要模拟整个硬件环境 和系统 很大。
![](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170502-1493737075229036266.jpg ':size=500')

Linux 操作系统由内核空间和用户空间组成。内核空间是 `kernel`，Linux 刚启动时会加载 `bootfs` 文件系统，之后 bootfs 会被卸载掉。
用户空间的文件系统是 `rootfs`，包含我们熟悉的 /dev, /proc, /bin 等目录。
对于 base 镜像来说，底层直接用 Host 的 kernel，自己只需要提供 rootfs 就行了。
![](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170423-1492906037945025377.jpg)
所有容器**共享同一个Host OS**，所以体积要比虚拟机小很多，而且启动容器不需要再启动一个操作系统所以容器部署和启动**速度更快**，**开销更小**，**更容易迁移**。

## 原理

* Docker架构
  ![](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170425-1493117446353024350.jpg)
  Docker 采用的是**Client/Server 架构**。客户端向服务器发送请求，服务器负责构建、运行和分发容器。客户端和服务器可以运行在同一个 Host 上，客户端也可以通过 socket 或 REST API 与远程的服务器通信。

容器的底层实现技术。
`cgroup` 和 `namespace` 是最重要的两种技术。`cgroup` 实现资源限额， `namespace` 实现资源隔离。

## 常用命令

* 本地镜像管理
  `docker images`
  `docker build`
  `docker tag`
  `docker rmi`
  `docker history` 镜像构造历史
* 仓库Registry
  `docker pull`
  `docker push`
  `docker login`

* 容器 
  `docekr run ` `docker run -d -p 82:8080 tomcat`   -m -c 
  `docekr start/stop/restart pause/unpause`
  `docker exec` `docker exec -i -t 31647c341238  bash`
   -it 以交互模式打开  exec 则是在容器中打开新的终端，并且可以启动新的进程。
  `docker attach`  
  attach 直接进入容器 启动命令 的终端，不会启动新的进程，如果想直接在终端中查看启动命令的输出，用 attach；其他情况使用 exec。
  `docker kill`
  `docker rm`

`docker ps`
`docker logs`

## DockerFile

构建镜像的两种方式 

1. `docker commit `
2. 编写DockerFile

* 新镜像是从 base 镜像一层一层叠加生成的 **最大的一个好处就是 - 共享资源**
* **Copy-on-Write 特性** 当容器启动时，一个新的可写层被加载到镜像的顶部。
  这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”。

![](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170516-1494943681160021117.jpg)

* `FROM scratch`
  此镜像是从白手起家，从 0 开始构建。

* `COPY` `ADD` 都是复制  `ADD` 会自动解压
* `RUN`:执行命令并创建新的Image layer，RUN 经常用于安装软件包。
* `CMD`:设置容器启动后默认执行的命令和参数， 但 CMD 能够被 `docker run` 后面跟的命令行参数替换。
* `ENTRYPOINT`:设置容器启动时运行的命令
* `RUN` 为了美观 已经 避免产生过多中间层 `RUN`命令尽量使用&&写成一行并使用\分割
* `WORKDIR` 尽量使用绝对目录
* `ENV`设置环境变量,设置环境变量，环境变量可被后面的指令使用
* `EXPOSE` 暴露端口 这里暴露端口只是让别人知道暴露了什么端口，不起实际作用。真正起作用是在 run -p 
* `VOLUME` 卷

## 网络

### 单机网络

* none

封闭网络。适用于不需要联网的安全性要求较高的场景。

* host

连接到 host 网络的容器共享 Docker host 的网络栈，容器的网络配置与 host 完全一样
直接使用 Docker host 的网络最大的好处就是性能，如果容器对网络传输效率有较高要求，则可以选择 host 网络。当然不便之处就是牺牲一些灵活性，比如要考虑端口冲突问题，Docker host 上已经使用的端口就不能再用了。
![1](http://7xo6kd.com1.z0.glb.clouddn.com/upload-ueditor-image-20170622-1498131142416099708.jpg ':size=300')

* brige

`docker network inspect bridge`

`docker network create --driver bridge --subnet 177.22.16.0/24 --gateway 177.22.16.1 my_net2`

只有使用 --subnet 创建的网络才能指定静态 IP。
`docker run -d --network=my_net2 --ip 177.22.16.8 httpd` 

为容器添加一块网卡
` docker network connect my_net2 d6d3b182107d`

## 存储

### 单Host存储

1.由 storage driver 管理的镜像层和容器层。

2.Data Volume。

 |	|bind mount|docker managed volume
 |----|----|---
volume 位置|	可任意指定|	/var/lib/docker/volumes/...
对已有mount point 影响|	隐藏并替换为 volume	|原有数据复制到 volume
是否支持单个文件	|支持	|不支持，只能是目录
权限控制	|可设置为只读，默认为读写权限	|无控制，均为读写权限
移植性	|移植性弱，与 host path 绑定	|移植性强，无需指定 host 目录

## Docker 三剑客

`Docker Compose`：是用来组装多容器应用的工具，可以在 Swarm集群中部署分布式应用。
`Docker Machine`：是支持多平台安装Docker的工具，使用 Docker Machine，可以很方便地在笔记本、云平台及数据中心里安装Docker。
`Docker Swarm`：是Docker社区原生提供的容器集群管理工具。