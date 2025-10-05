I am running Home Assistant on a Raspberry Pi in a docker container.



Matter 使用一个基于 IP 的协议栈，支持以下几种网络传输方式：

Wi-Fi
Thread
以太网

## Required Hardware

How To Add Bluetooth Support

BLE 适配器 在 Matter 中仅仅只是承担辅助配网的角色.Bluetooth used during commissioning 


### Required Hardware For The ESPHome Bluetooth Proxy

Bluetooth Proxy In Home Assistant Using ESPHome

https://www.simplysmart.house/blog/bluetooth-proxy-home-assistant-epshome





Docker Matter Server

I have flashed my sonoff dongle-e with an openthread firmware (thread only). I believe this is the same situation like you. The dongle will act as a border router. 

## Docker containers:

- homeassistant container

- openthread/otbr container -->run OTBR on the pi using docker
connect thread border router to the local network

Chạy Docker OTBR  |  OpenThread

Thread 设备
Thread 设备向 Thread 边界路由器注册自己的服务，接着 Thread 边界路由器通过多播 DNS 向 Wi-Fi 网络广播所有 Thread 设备的服务信息。

Thread 边界路由器实现了 DNS-SD 发现代理 (Discovery Proxy)，这样 Thread 设备也可以发现 Wi-Fi 网络中的服务。

- python-matter-server container

matter controller server = matter add-on

GitHub - home-assistant-libs/python-matter-server: Python server to interact with Matter

## Intergrations:

1. open thread border router integration -->connect thread border router to the local network
use http://localhost:8081 by default to connect to the otbr container.
负责建立docker otbr 和ha之间的通信

Autodiscover Thread after enabling the OTBR integration http://localhost:8081

~~~
Provide URL for the OpenThread Border Router's REST API：http://192.168.2.125:8081
~~~

2. Thread integration
used to create thread network, border router must be assigned to the homeassistant thread network

3. Matter integration
connect to the matter container, default websocket address doesn’t need to be changed for setup

When all of these are configured correctly, you can add matter devices with the homeassistant app on your smart phone.

https://community.home-assistant.io/t/using-matter-and-thread-in-a-dockerized-ha-instance/721088/7?u=msly




## Required Software


docker pull ghcr.io/home-assistant-libs/python-matter-server:stable

~~~
docker run -d \
  --name matter-server \
  --restart=unless-stopped \
  --security-opt apparmor=unconfined \
  -v $(pwd)/data:/data \
  --network=host \
  ghcr.io/home-assistant-libs/python-matter-server:stable
~~~


3. Matter server 
	- [HA Docker with SLZB-07Mg24 Matter/Thread USB](https://community.home-assistant.io/t/ha-docker-with-slzb-07mg24-matter-thread-usb/834547)  
	- [SLZB-07Mg24 USB stick](https://community.home-assistant.io/t/running-otbr-in-docker/835125)
	- [VMware + Ubuntu 22.04](https://blog.csdn.net/xingzhibo/article/details/132333807)   VMware + Ubuntu 22.04
	- [VirtualBox + Ubuntu 22.04](https://www.matterxiaomi.com/blog/matter-gateway-part-2//blog/matter-gateway-part-2/) VirtualBox (with Ubuntu 20.04 LTS) installed on Windows 10. 
	- [mDNS系列](https://www.iaspnetcore.com/blog/tag/mDNS)
	- [ghcr.io/ownbee/hass-otbr-docker](ghcr.io/ownbee/hass-otbr-docker)


## docker OTBR 

在rpi 5，使用 docker 直接拉取官方配置好的OTBR Addon image,修改为docker版

amd64

https://github.com/ownbee/hass-otbr-docker
ghcr.io/ownbee/hass-otbr-docker

arm64 and amd64
	
https://github.com/D34DC3N73R/hass-otbr-docker
ghcr.io/d34dc3n73r/hass-otbr-docker

other

目前 Matter 在海外得到几乎所有大的生态平台厂家的支持，包括：
Apple
Google
Amazon
Samsung
Philips Hue

