
## Install Esphome in a docker container

docker pull ghcr.io/esphome/esphome:stable

mkdir /data/docker/esphome


~~~
$ docker pull ghcr.io/esphome/esphome
$ docker run --rm --net=host --name esphome -v /home/user/esphome/:/config -d ghcr.io/esphome/esphome
~~~


sudo ufw allow 6052


we can access ESPHome by typing our server address and port 6052 in our browser: http://192.168.1.3:6052


Useful links

Complete Docker ESPHome Installation Guide

https://www.msly.cn/boards/topic/38216/complete-docker-esphome-installation-guide

https://www.matterxiaomi.com/boards/topic/40237/docker-esphome-using-docker-compose

https://chelmiki.com/posts/installing-and-configuring-esphome/