
## Install Esphome in a docker container

docker pull ghcr.io/esphome/esphome:stable

mkdir /data/docker/esphome


~~~
$ docker pull ghcr.io/esphome/esphome:stable
$ docker run --rm --net=host --name esphome -v /data/docker/esphome/:/config -d ghcr.io/esphome/esphome

sudo ufw allow 6052
~~~


# docker compose version
Docker Compose version v2.29.7

~~~
sudo apt install docker-compose

cd /data/docker/esphome
docker compose up -d
~~~

we can access ESPHome by typing our server address and port 6052 in our browser: http://192.168.1.3:6052


Useful links

Complete Docker ESPHome Installation Guide

https://www.msly.cn/boards/topic/38216/complete-docker-esphome-installation-guide

https://www.matterxiaomi.com/boards/topic/40237/docker-esphome-using-docker-compose

Guide:

https://chelmiki.com/posts/installing-and-configuring-esphome/

