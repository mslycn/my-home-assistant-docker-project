### 启动镜像
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /dockerData/portainer:/data --restart=always --name portainer portainer/portainer-ce:latest

### 访问http://ip:9000


https://blog.csdn.net/weixin_44649780/article/details/128401975