docker images

https://hub.docker.com/r/bmartin5692/bumper

docker pull docker pull bmartin5692/bumper

~~~
docker run -it -e "BUMPER_ANNOUNCE_IP=X.X.X.X" -p 443:443 -p 8007:8007 -p 8883:8883 -p 5223:5223 -v /home/user/bumper/data:/bumper/data --name bumper bmartin5692/bumper
~~~


Useful links

https://www.home-assistant.io/integrations/ecovacs

https://bumper.readthedocs.io/en/latest/


- docker bumper
https://bumper.readthedocs.io/en/latest/Docker/



