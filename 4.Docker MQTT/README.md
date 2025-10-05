在Docker环境下配置和搭建EMQXMQTT服务，包括获取镜像、端口映射、挂载目录、配置文件同步、容器管理以及客户端连接测试等步骤。

docker pull eclipse-mosquitto




- Install MQTT using Docker and Home Assistant
https://hometechhacker.com/mqtt-using-docker-and-home-assistant/


docker run eclipse-mosquitto
docker run -it --rm  --name "mosquitto"  -p 1883:1883 eclipse-mosquitto

raspberrypi:/datadocker/mosquitto/config# find / -name mosquitto.conf

output
~~~
/datadocker/mosquitto/config/mosquitto.conf
/var/lib/docker/rootfs/overlayfs/0f196d38203ec169b9478a0d32ff457ae909157a88ef8e97795dfee4320c7ae7/mosquitto/config/mosquitto.conf
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/98/fs/mosquitto/config/mosquitto.conf
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/32/fs/mosquitto/config/mosquitto.conf
raspberrypi:/datadocker/mosquitto/config# find / -name mosquitto.conf
~~~

docker run eclipse-mosquitto cancle
docker run -it --rm  --name "mosquitto"  -p 1883:1883 eclipse-mosquitto 


/datadocker/mosquitto/config/mosquitto.conf
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/32/fs/mosquitto/config/mosquitto.conf

port:1883
