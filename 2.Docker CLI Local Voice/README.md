
Ubuntu 22.04.5 LTS on vultr

lsb_release -a
~~~
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 22.04.5 LTS
Release:	22.04
Codename:	jammy
~~~

## step 1.Docker run wyoming-piper  wyoming-whisper  wyoming-openwakeword


~~~
docker run -it -p 10200:10200 -v /path/to/local/data:/data rhasspy/wyoming-piper     --voice en_US-lessac-medium
docker run -it -p 10300:10300 -v /path/to/local/data:/data rhasspy/wyoming-whisper     --model tiny-int8 --language en
docker run -it -p 10400:10400 rhasspy/wyoming-openwakeword     --preload-model 'ok_nabu'
~~~

docker ps -a

output
~~~
CONTAINER ID   IMAGE                          COMMAND                  CREATED         STATUS         PORTS                                           NAMES
1ee50dbb7a33   rhasspy/wyoming-piper          "bash /run.sh --voic…"   7 minutes ago   Up 7 minutes   0.0.0.0:10200->10200/tcp, :::10200->10200/tcp   nice_hofstadter
01b832193e61   rhasspy/wyoming-openwakeword   "bash /run.sh --prel…"   7 hours ago     Up 7 hours     0.0.0.0:10400->10400/tcp, :::10400->10400/tcp   gallant_engelbart
0389595d9f22   rhasspy/wyoming-whisper        "bash /run.sh --mode…"   8 hours ago     Up 8 hours     0.0.0.0:10300->10300/tcp, :::10300->10300/tcp   nostalgic_jang
~~~

## step 2.Wyoming Protocol Integration

integrate all of above to home assistant via  Wyoming Protocol Integration

所有服务启动后，需要在 Home Assistant 中安装集成

http://192.168.2.50:8123/config/integrations/integration/wyoming


## step 3.Voice assistants
create a Voice assistants named with test  for EspHome ESP32-S3-BOX3B


## step 4.EspHome  ESP32-S3-BOX3B voice assistant

Configure  EspHome  ESP32-S3-BOX3B use test voice assistant as defalut voice assistant

## test

test  audio

I tied to let bing.com say ‘ok nabu’ - typed ‘ok nabu’ - and it says ‘Okey nabu’ - It  works fine.

so letting bing.com say  ‘turn on the office light’ and the ligt is turned on, and box-3 is responding - chaining screens.

It all works fine…

ok nabu 发音
https://cn.bing.com/translator/?ref=TThis&text=nabu+english+study&from=en&to=ZH-HANS

turn off the light







## OpenAI的Whisper模型

## faster-whisper

faster-whisper是基于OpenAI的Whisper模型的实现。faster-whisper的核心优势在于其能够在保持原有模型准确度的同时，大幅提升处理速度，。

https://github.com/SYSTRAN/faster-whisper

## wyoming-faster-whisper

wyoming-faster-whisper 是基于faster-whisper模型添加wyoming协议的实现。wyoming协议为home assistant自动发现所用。

Wyoming protocol server for the faster-whisper[https://github.com/SYSTRAN/faster-whisper] speech to text system.

https://github.com/rhasspy/wyoming-faster-whisper