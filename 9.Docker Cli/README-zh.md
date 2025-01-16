
docker system df -v 

~~~
CONTAINER ID   IMAGE                                                     COMMAND                  LOCAL VOLUMES   SIZE      CREATED       STATUS                     NAMES
96f33b12827f   e20ca1d7b578                                              "/init /bin/bash top"    0               4.1kB     6 days ago    Exited (126) 6 days ago    magical_ganguly
2bd1aea2de2d   e20ca1d7b578                                              "/init"                  0               60.5MB    2 weeks ago   Up 19 hours                ha
437ff8679ca7   rhasspy/wyoming-piper                                     "bash /run.sh --voic…"   0               20.5kB    5 weeks ago   Exited (255) 3 days ago    romantic_chebyshev
4c8a84170a3a   ghcr.io/home-assistant-libs/python-matter-server:stable   "matter-server --sto…"   0               389kB     5 weeks ago   Exited (137) 2 weeks ago   matter-server

~~~


1. Docker存储结构 /var/lib/docker

在开始清理之前，了解Docker的存储结构。/var/lib/docker 目录主要包含以下内容：
~~~
Images：存储Docker镜像。
Containers：存储运行中的容器和停止的容器。
Volumes：存储持久化数据。
Networks：存储自定义网络。
Plugins：存储插件。
~~~

手动清理

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


2. 查看 Docker 容器、镜像、卷等资源的占用情况
docker system df

~~~
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          6         2         5.806GB   2.732GB (47%)
Containers      4         1         60.92MB   413.7kB (0%)
Local Volumes   0         0         0B        0B
Build Cache     0         0         0B        0B

~~~



## /var/run/docker/containerd

containerd is just a container daemon. Doesn’t care about images.

sudo du -h --max-depth=1 /var/lib/ | sort -hr

https://docs.dockerd.com.cn/reference/cli/docker/config/create/




## Docker磁盘空间管理

https://www.cnblogs.com/deali/p/18612139




~~~
sudo git push -u origin main
~~~

 cpu 100%
~~~
top
top - 22:42:51 up 7 min,  3 users,  load average: 0.58, 0.56, 0.35
Tasks: 151 total,   2 running, 149 sleeping,   0 stopped,   0 zombie
%Cpu(s): 26.0 us,  0.6 sy,  0.0 ni, 73.2 id,  0.1 wa,  0.0 hi,  0.2 si,  0.0 st 
MiB Mem :    907.3 total,    291.7 free,    350.2 used,    322.1 buff/cache     
MiB Swap:    200.0 total,    150.0 free,     50.0 used.    557.1 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                      
   1726 root      20   0  445176 171832   4636 R 100.0  18.5   0:27.94 git                                          
    710 nobody    20   0  723272  12560   5504 S   5.0   1.4   0:07.52 frpc                                         
   1527 root      20   0   11712   4864   2816 R   1.0   0.5   0:02.03 top                                          
    236 root      20   0   49956  12928  12288 S   0.3   1.4   0:02.22 systemd-journal                              
    474 avahi     20   0    7360   2944   2560 S   0.3   0.3   0:00.72 avahi-daemon                                 
   1621 root      20   0       0      0      0 I   0.3   0.0   0:00.01 kworker/u12:0-writeback                      
      1 root      20   0  168544   9316   7452 S   0.0   1.0   0:07.41 systemd     


~~~