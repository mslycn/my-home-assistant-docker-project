

docker pull portainer/portainer

docker manifest inspect portainer/portainer 
~~~
{
         "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
         "size": 1154,
         "digest": "sha256:4b07db37993e409a73c723539343e310d21e9666a2ccac1dce1258f6a05f7186",
         "platform": {
            "architecture": "arm64",
            "os": "linux"
         }
      },

~~~


### 启动镜像
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /dockerData/portainer:/data --restart=always --name portainer portainer/portainer-ce:latest



### 访问http://ip:9000


https://blog.csdn.net/weixin_44649780/article/details/128401975

http://iotts.com.cn/course/docker/Docker%E8%BD%BB%E9%87%8F%E7%BA%A7%E5%9B%BE%E5%BD%A2%E9%A1%B5%E9%9D%A2%E7%AE%A1%E7%90%86Portainer%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/

