# Nextcloud  

https://github.com/nextcloud

https://github.com/nextcloud/docker

https://github.com/nextcloud/docker/releases



1. Download
## For ARM CPUs
docker pull --platform linux/arm64 nextcloud:latest  arm

2. docker run
~~~
$ docker run -d \
-v nextcloud:/var/www/html \
nextcloud
~~~

Note

/var/www/html/ folder where all Nextcloud data lives

3. visit
https://192.168.2.50:8080

4. login




useful links

Docker + Nextcloud + MySQL + ONLYOFFICE

https://blog.csdn.net/yijian0645/article/details/137109351








