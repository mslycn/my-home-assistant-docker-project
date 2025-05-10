
docker pull eclipse-mosquitto




- Install MQTT using Docker compose and Home Assistant
https://sequr.be/blog/2022/09/home-assistant-container-part-4-mosquitto-docker-container/


docker-compose.yaml
~~~
services:
 
  mosquitto:
    container_name: mosquitto
    image: eclipse-mosquitto
    restart: unless-stopped
    ports:
      - "1883:1883/tcp"
    environment:
      - TZ=Europe/Brussels
    volumes:
      - /datadocker/mosquitto/config:/mosquitto/config
      - /datadocker/mosquitto/data:/mosquitto/data
      - /datadocker/mosquitto/log:/mosquitto/log
    stdin_open: true
    tty: true


~~~



cd /datadocker/mosquitto

docker-compose up

or

docker compose up -d



cd /datadocker/mosquitto/config/
sudo wget https://raw.githubusercontent.com/eclipse/mosquitto/master/mosquitto.conf

vi mosquitto.conf

~~~

# Listen on port 1883 on all IPv4 interfaces
listener 1883
socket_domain ipv4
# save the in-memory database to disk
persistence true
persistence_location /mosquitto/data/
# Log to stderr and logfile
log_dest stderr
log_dest file /mosquitto/log/mosquitto.log
# Require authentication
allow_anonymous true
~~~


docker compose restart mosquitto


