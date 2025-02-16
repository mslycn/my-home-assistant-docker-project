My Configuration

Homeassistant Docker 2025.1.4  on rpi 
ESPhome installed also via docker
ESP32-S3-BOX-3B



# Chapter 1 - Systems without an NVidia GPU

This article explains how to Run whisper piper and wakeword with docker cli on external server.

Install Whisper and start the docker with the default model “tiny-int8”.
Install piper and start it
Install openwakeword and start it


# Setting Up Whisper and Piper with Docker on Linux

Setting up a fully local voice assistant.Local Install via Docker Cli

Ubuntu 22.04.5 LTS on vultr.

I’m running it on Ubuntu 20.04 server



## OS

lsb_release -a
~~~
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 22.04.5 LTS
Release:	22.04
Codename:	jammy
~~~

## Install Requirements 

64bit OS only

Install Docker on Linux

Download and install Docker from the official Docker website.



~~~
sudo docker pull rhasspy/wyoming-piper
sudo docker pull rhasspy/wyoming-whisper
sudo docker pull rhasspy/wyoming-openwakeword
~~~


## step 1.Docker run wyoming-piper  wyoming-whisper  wyoming-openwakeword


~~~
docker run -it -p 10200:10200 -v /path/to/local/data:/data rhasspy/wyoming-piper     --voice en_US-lessac-medium
docker run -it -p 10300:10300 -v /path/to/local/data:/data rhasspy/wyoming-whisper     --model tiny-int8 --language en
docker run -it -p 10400:10400 rhasspy/wyoming-openwakeword     --preload-model 'ok_nabu'
~~~
Note

Adjust /path/to/local/data  to a directory on your Linux machine where Whisper can store its model data.


docker ps -a

output
~~~
CONTAINER ID   IMAGE                          COMMAND                  CREATED         STATUS         PORTS                                           NAMES
1ee50dbb7a33   rhasspy/wyoming-piper          "bash /run.sh --voic…"   7 minutes ago   Up 7 minutes   0.0.0.0:10200->10200/tcp, :::10200->10200/tcp   nice_hofstadter
01b832193e61   rhasspy/wyoming-openwakeword   "bash /run.sh --prel…"   7 hours ago     Up 7 hours     0.0.0.0:10400->10400/tcp, :::10400->10400/tcp   gallant_engelbart
0389595d9f22   rhasspy/wyoming-whisper        "bash /run.sh --mode…"   8 hours ago     Up 8 hours     0.0.0.0:10300->10300/tcp, :::10300->10300/tcp   nostalgic_jang
~~~

## step 2.Wyoming Protocol Integration

integrate all of above to home assistant via  Wyoming Protocol Integration.

looking at Home Assistant's Whisper integration.

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

**Useful links**

Part 1 - Local Voice in Home Assistant core

https://blog.matterxiaomi.com/blog/voice-homeassistant/

Part 2 - Run whisper on external server

https://blog.matterxiaomi.com/blog/run-whisper-on-external-server/

Part 3 - Run piper on external server

https://blog.matterxiaomi.com/blog/run-piper-on-external-server/

Part 4 - Run wakeword on external server

https://blog.matterxiaomi.com/blog/run-wakeword-on-external-server/




## penAI Whisper vs faster-whisper vs wyoming-faster-whisper vs whisper add on

### OpenAI的Whisper模型

https://github.com/OpenAI/whisper

### faster-whisper

faster-whisper is a reimplementation of OpenAI's Whisper model using CTranslate2, which is a fast inference engine for Transformer models. This implementation is up to 4 times faster than openai/whisper for the same accuracy while using less memory. The efficiency can be further improved with 8-bit quantization on both CPU and GPU.

faster-whisper是基于OpenAI的Whisper模型的实现。faster-whisper的核心优势在于其能够在保持原有模型准确度的同时，大幅提升处理速度。是一个使用 CTranslate2 重新实现的 OpenAI Whisper 模型，旨在提高转录速度和效率。

它显著提高了处理速度，与原始 Whisper 模型相比，保持了相同的准确性的同时，速度提升了最多 4 倍，并且降低了内存使用量。

此外，它支持 CPU 和 GPU 上的 8 位量化，进一步优化效率。

https://github.com/SYSTRAN/faster-whisper

### wyoming-faster-whisper

wyoming-faster-whisper 是基于faster-whisper模型添加wyoming协议的实现。wyoming协议为home assistant自动发现所用。

Wyoming protocol server for the faster-whisper[https://github.com/SYSTRAN/faster-whisper] speech to text system.

https://github.com/rhasspy/wyoming-faster-whisper





Useful links


1. https://github.com/SYSTRAN/faster-whisper项目介绍

https://www.cnblogs.com/ghj1976/p/18034191/fasterwhisper





