I am running Home Assistant on a Raspberry Pi in a docker container.

目前 Matter 在海外得到几乎所有大的生态平台厂家的支持，包括：
Apple
Google
Amazon
Samsung
Philips Hue

Matter 使用一个基于 IP 的协议栈，支持以下几种网络传输方式：

Wi-Fi
Thread
以太网

而 BLE 在 Matter 中目前仅仅只是承担辅助配网的角色


Docker Matter Server


I have flashed my sonoff dongle-e with an openthread firmware (thread only). I believe this is the same situation like you. The dongle will act as a border router. Here are what I have:

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

- open thread border router integration -->connect thread border router to the local network
use http://localhost:8081 by default to connect to the otbr container.

- Thread integration
used to create thread network, border router must be assigned to the homeassistant thread network

- Matter integration
connect to the matter container, default websocket address doesn’t need to be changed for setup

When all of these are configured correctly, you can add matter devices with the homeassistant app on your smart phone.

https://community.home-assistant.io/t/using-matter-and-thread-in-a-dockerized-ha-instance/721088/7?u=msly


## Required Hardware

How To Add Bluetooth Support



### Required Hardware For The ESPHome Bluetooth Proxy

Bluetooth Proxy In Home Assistant Using ESPHome

https://www.simplysmart.house/blog/bluetooth-proxy-home-assistant-epshome


## Required Software


docker pull ghcr.io/home-assistant-libs/python-matter-server:stable


docker run -d \
  --name matter-server \
  --restart=unless-stopped \
  --security-opt apparmor=unconfined \
  -v $(pwd)/data:/data \
  --network=host \
  ghcr.io/home-assistant-libs/python-matter-server:stable



3. Matter server 
	- [HA Docker with SLZB-07Mg24 Matter/Thread USB](https://community.home-assistant.io/t/ha-docker-with-slzb-07mg24-matter-thread-usb/834547)  
	- [SLZB-07Mg24 USB stick](https://community.home-assistant.io/t/running-otbr-in-docker/835125)
	- [VMware + Ubuntu 22.04](https://blog.csdn.net/xingzhibo/article/details/132333807)   VMware + Ubuntu 22.04
	- [VirtualBox + Ubuntu 22.04](https://www.matterxiaomi.com/blog/matter-gateway-part-2//blog/matter-gateway-part-2/) VirtualBox (with Ubuntu 20.04 LTS) installed on Windows 10. 
	- [mDNS系列](https://www.iaspnetcore.com/blog/tag/mDNS)
	- [ghcr.io/ownbee/hass-otbr-docker](ghcr.io/ownbee/hass-otbr-docker)


在rpi 5，使用 docker 直接拉取官方配置好的OTBR Addon image,修改为docker版

amd64

https://github.com/ownbee/hass-otbr-docker
ghcr.io/ownbee/hass-otbr-docker

arm64 and amd64
	
https://github.com/D34DC3N73R/hass-otbr-docker
ghcr.io/d34dc3n73r/hass-otbr-docker

