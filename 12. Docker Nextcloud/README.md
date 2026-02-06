# Nextcloud

https://github.com/nextcloud

https://github.com/nextcloud/docker



1. Download
## For ARM CPUs
docker pull ghcr.io/nextcloud-releases/all-in-one  arm

2. docker run
~~~
# For Linux and without a web server or reverse proxy (like Apache, Nginx, Caddy, Cloudflare Tunnel and else) already in place:
sudo docker run \
--init \
--sig-proxy=false \
--name nextcloud-aio-mastercontainer \
--restart always \
--publish 80:80 \
--publish 8080:8080 \
--publish 8443:8443 \
--volume nextcloud_aio_mastercontainer:/mnt/docker-aio-config \
--volume /var/run/docker.sock:/var/run/docker.sock:ro \
ghcr.io/nextcloud-releases/all-in-one:latest
~~~

3. visit
https://192.168.2.50:8080

4. login





## nextcloud

https://github.com/nextcloud/docker/releases

docker pull --platform linux/arm64 nextcloud:2025.12.1


docker pull --platform linux/arm64 nextcloud:latest

docker manifest inspect <镜像名称>

docker manifest inspect nextcloud:latest


~~~
$ docker run -d \
-v nextcloud:/var/www/html \
nextcloud
~~~

Note

/var/www/html/ folder where all Nextcloud data lives