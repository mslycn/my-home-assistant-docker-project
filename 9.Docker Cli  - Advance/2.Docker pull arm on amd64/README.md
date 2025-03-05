# Docker：使用x86平台Docker 拉取 arm版镜像 

使用镜像创建一个容器，该镜像必须与 Docker 宿主机系统架构一致，例如x86_64 架构的系统中只能使用x86_64的镜像创建容器。

docker manifest特性可支持用户在不同系统架构的机器上分别运行不同的架构的镜像。这一点基本不需要用户做任何适配，非常的方便。

manifest list是一个镜像清单列表，用于存放多个不同os/arch的镜像信息；主要用到manifest的目的，其实还是多用于存放不同的os/arch信息，也就是方便我们在不同的CPU架构（arm或者x86）或者操作系统中，通过一个镜像名称拉取对应架构或者操作系统的镜像

## 拉取指定平台镜像
~~~
#X86平台docker拉取arm镜像
docker pull --platform=arm64 镜像名:版本

#示例
docker pull --platform=arm64 nginx:latest
~~~

使用 docker pull 拉取特定架构amd64、arm64、aarch64的容器镜像

https://www.cnblogs.com/nhdlb/p/15233410.html

https://blog.csdn.net/cml011/article/details/128729136