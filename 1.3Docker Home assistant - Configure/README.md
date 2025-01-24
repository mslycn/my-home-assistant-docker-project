
## 使用 Docker Pull 自定义（指定）镜像源

通过在镜像名称前加上镜像源的 URL 来指定从镜像源下载镜像
~~~
$ docker pull registry.cn-hangzhou.aliyuncs.com/library/nginx
~~~



## 配置镜像加速器

除了在Docker pull 命令中直接指定镜像源，我们还可以通过配置 Docker 守护进程来永久设置默认的镜像源。下面是如何配置 Docker 镜像源的示例：

编辑 Docker 配置文件 /etc/docker/daemon.json
~~~
$ sudo nano /etc/docker/daemon.json
~~~

在配置文件中添加以下内容，其中 <mirror-url> 是你要使用的镜像源的 URL：
~~~
{
  "registry-mirrors": ["<mirror-url>"]
}
~~~
重启 Docker 守护进程以使配置生效
~~~
$ sudo systemctl restart docker
~~~



针对Docker客户端版本大于 1.10.0 的用户

可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器

### aliyun镜像源

获取aliyun镜像源

menu path：容器镜像服务/镜像加速器
https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors

First, edit your /etc/docker/daemon.json file (create it if it doesn't exist using sudo) and add the following content:
~~~
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://iao.mirror.aliyuncs.com"]
}
EOF
~~~

Next, restart your Docker daemon by running:

通过修改 dockerd 配置文件，并重载，可以在服务器上开启 dockerd 的属性

~~~
sudo systemctl daemon-reload
sudo systemctl restart docker
~~~

### nju镜像源

使用的容器需要从github下载镜像，服务器在国外下载速度很慢，提供镜像加速的方案

sudo vim /etc/docker/daemon.json

~~~
{
  "registry-mirrors": ["https://ghcr.nju.edu.cn"]
}
~~~
