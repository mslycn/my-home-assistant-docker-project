
## Required Hardware

How To Add Bluetooth Support



### Required Hardware For The ESPHome Bluetooth Proxy

Bluetooth Proxy In Home Assistant Using ESPHome

https://www.simplysmart.house/blog/bluetooth-proxy-home-assistant-epshome


## Required Software


I have flashed my sonoff dongle-e with an openthread firmware (thread only). I believe this is the same situation like you. The dongle will act as a border router. Here are what I have:

## Docker containers:

- homeassistant container

- openthread/otbr container
connect thread border router to the local network
Chạy Docker OTBR  |  OpenThread

- python-matter-server container
matter controller server = matter add-on
GitHub - home-assistant-libs/python-matter-server: Python server to interact with Matter

## Intergrations:

- open thread border router integration
not sure if it’s really necessary, use http://localhost:8081 by default to connect to the otbr container. (don’t know if this port 8081 can be changed)

- Thread integration
used to create thread network, border router must be assigned to the homeassistant thread network

- Matter integration
connect to the matter container, default websocket address doesn’t need to be changed for setup

When all of these are configured correctly, you can add matter devices with the homeassistant app on your smart phone.

https://community.home-assistant.io/t/using-matter-and-thread-in-a-dockerized-ha-instance/721088/7?u=msly




