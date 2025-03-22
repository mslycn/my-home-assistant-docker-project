I am running Home Assistant on a Raspberry Pi in a docker container.

Docker Matter Server


I have flashed my sonoff dongle-e with an openthread firmware (thread only). I believe this is the same situation like you. The dongle will act as a border router. Here are what I have:

## Docker containers:

- homeassistant container

- openthread/otbr container -->run OTBR on the pi using docker
connect thread border router to the local network
Chạy Docker OTBR  |  OpenThread

Thread 设备
Thread 设备向 Thread 边界路由器注册自己的服务，接着 Thread 边界路由器通过多播 DNS 向 Wi-Fi 网络广播所有 Thread 设备的服务信息。

Thread 边界路由器还实现了 DNS-SD 发现代理 (Discovery Proxy)，这样 Thread 设备也可以发现 Wi-Fi 网络中的服务。

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






