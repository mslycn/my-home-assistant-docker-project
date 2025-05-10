## containerd vs containerd  | What are the differences?

- docker和containerd 的工作目录默认都在 /var/lib 下

- Docker与containerd的关系与区别 

Docker和containerd的不同之处在于它们的范围：Docker是一个完整的容器化平台，提供了构建、部署和运行容器的工具，而containerd是一个更轻量级的运行时，专注于管理容器的生命周期.

Docker 实际上是由多个组件构成的，其中之一就是 containerd。

从 Docker 1.11 版本开始，Docker 的容器运行时部分（即实际负责启动、停止、管理容器的部分）由 containerd 承担。因此，containerd 是 Docker 内部的一个组件，负责容器的生命周期管理（如启动、停止、暂停等）。

1.2  containerd 的功能

containerd 是一个 容器运行时（Container Runtime），专注于容器的生命周期管理，不包含构建镜像、容器编排等功能。它提供了容器的管理功能（如容器创建、启动、停止、删除）以及镜像的拉取、存储等基础功能。containerd 是一个轻量级、专注于容器管理的工具，适用于容器编排系统（如 Kubernetes）和大型生产环境。

1.3 Docker 的功能

Docker 是一个包含了完整工具链的容器管理平台，不仅包括容器运行时（containerd 提供的功能），还包括镜像构建、镜像管理、容器编排、CI/CD 集成等功能。Docker 使用 containerd 作为容器运行时，但它封装了更多的功能（如镜像构建、容器编排、网络管理等），使得用户能够更加方便地管理容器应用。简而言之，containerd 是 Docker 的底层容器运行时，它提供容器启动、停止等管理功能，而 Docker 提供了更加丰富的工具和接口（如镜像构建、容器编排、应用发布等），使得用户能够以更简单的方式管理容器化应用。（containerd是docker的一个底层服务，但docker并不是只有这一个底层服务，而是有多个底层服务。）

https://www.cnblogs.com/junnan/p/18589605


docker system df -v 

~~~
CONTAINER ID   IMAGE                                                     COMMAND                  LOCAL VOLUMES   SIZE      CREATED       STATUS                     NAMES
96f33b12827f   e20ca1d7b578                                              "/init /bin/bash top"    0               4.1kB     6 days ago    Exited (126) 6 days ago    magical_ganguly
2bd1aea2de2d   e20ca1d7b578                                              "/init"                  0               60.5MB    2 weeks ago   Up 19 hours                ha
437ff8679ca7   rhasspy/wyoming-piper                                     "bash /run.sh --voic…"   0               20.5kB    5 weeks ago   Exited (255) 3 days ago    romantic_chebyshev
4c8a84170a3a   ghcr.io/home-assistant-libs/python-matter-server:stable   "matter-server --sto…"   0               389kB     5 weeks ago   Exited (137) 2 weeks ago   matter-server

~~~

## /var/lib/docker

1. Docker存储结构 /var/lib/docker

在开始清理之前，了解Docker的存储结构。/var/lib/docker 目录主要包含以下内容：
~~~
Images：存储Docker镜像。
Containers：存储运行中的容器和停止的容器。
Volumes：存储持久化数据。
Networks：存储自定义网络。
Plugins：存储插件。
~~~

2. 查看 Docker 容器、镜像、卷等资源的占用情况

docker system df

~~~
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          6         2         5.806GB   2.732GB (47%)
Containers      4         1         60.92MB   413.7kB (0%)
Local Volumes   0         0         0B        0B
Build Cache     0         0         0B        0B

~~~

Overlay2是Docker的存储驱动，用来管理镜像和容器的分层文件系统。当用户使用Docker时，所有的镜像层和容器层都是通过overlay2来处理的，所以这个目录可能会变得很大。

##
清理Docker的空间应该使用Docker自带的命令，比如docker system prune


## 手动清理

可以手动删除/var/lib/docker 目录下的文件和文件夹。

# 删除Images
rm -rf /var/lib/docker/images/*

# 删除Containers
rm -rf /var/lib/docker/containers/*

# 删除Volumes
rm -rf /var/lib/docker/volumes/*

# 删除Networks
rm -rf /var/lib/docker/networks/*

# 删除Plugins
rm -rf /var/lib/docker/plugins/*


## 彻底清理 Overlay2
如果确定所有容器和镜像均无用，可彻底重置 Docker：
~~~
# 停止 Docker 服务
sudo systemctl stop docker

# 删除所有 Docker 数据（包括镜像、容器、卷等）
sudo rm -rf /var/lib/docker/*

# 重启 Docker
sudo systemctl start docker
~~~


## /var/run/docker/containerd

containerd is just a container daemon. Doesn’t care about images.

sudo du -h --max-depth=1 /var/lib/ | sort -hr

https://docs.dockerd.com.cn/reference/cli/docker/config/create/




## Docker磁盘空间管理

清空一个特定容器的日志文件：

sudo truncate -s 0 /var/lib/docker/containers/<container-id>/<container-id>-json.log

https://www.cnblogs.com/deali/p/18612139





