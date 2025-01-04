docker images

~~~
REPOSITORY                                         TAG       IMAGE ID       CREATED        SIZE
ghcr.io/home-assistant/home-assistant              stable    132ef461504b   13 days ago    2.65GB
<none>                                             <none>    e20ca1d7b578   2 weeks ago    2.65GB
ghcr.io/home-assistant-libs/python-matter-server   stable    e291154e44ac   3 months ago   695MB
m.daocloud.io/docker.io/nodered/node-red           latest    55fc57012066   3 months ago   823MB
ghcr.io/esphome/esphome                            latest    b8209dc73177   5 months ago   733MB
rhasspy/wyoming-piper                              latest    103222f9522b   55 years ago   74.6MB

~~~
解释：
~~~
REPOSITORY: 来自于哪个仓库；
TAG: 镜像的标签信息，比如 5.7、latest 表示不同的版本信息；
IMAGE ID: 镜像的 ID, 如果您看到两个 ID 完全相同，那么实际上，它们指向的是同一个镜像，只是标签名称不同罢了；如：allen_mysql:5.7 和 docker.io/mysql:5.7 的镜像 ID 是一模一样的，说明它们是同一个镜像，只是别名不同而已。
CREATED: 镜像最后的更新时间；
SIZE: 镜像的大小
~~~

