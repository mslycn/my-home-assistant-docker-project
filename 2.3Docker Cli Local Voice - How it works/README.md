# 原生的Home Assistant语音助理工作原理

This article explains how a customer can implement a local voice assistant.Local solution based on Whisper and Piper. 

First,you need to install those,  via  docker. Then piper is (by default) port 10200 and whisper (by default) port 10300.

Next,In the Wyoming integration popup you should put once piper host and port and adding a second Wyoming integration with whisper host and port.

You can select Voice Assistant Pipeline for recognition process:
~~~
Speaker(audio)=>WAKE(wakeword addon) =>audio=> STT（whipser addon） =>Conversation=>Intent recognition=>action=>Intent execution=> NLP(text ,openai)=> TTS(result piper)
~~~
https://www.matterxiaomi.com/boards/topic/14594/voice-in-home-assistant#20849

The Voice Assistant consists of the following  tools:

Esp32-s3-box3b is a ESPHome device with a microphone and a speaker.remote login program (SSH client).
sshd is an OpenSSH SSH daemon.
piper is a  remote tts program.
whisper is a remote stt  program.
Conversation is an authentication agent for caching private keys.
Speech-to-Text integration adds host ip and port to Home assistant.
ssh-keygen generates, manages, and converts authentication keys for ssh.
ssh-copy-id is a script that adds local public keys to the authorized_keys file on a remote SSH server.
ssh-keyscan gathers SSH public host keys.



Using Assist consists of：

targeting exposed devices and entities.

Assigned to areas


ESPHome device with a microphone

Wake word detection

saying supported commands

Speech to text

Intent Recognition
Intent Handling


Note

ESPHome device with a microphone = it

1. it detects the hot word

2. it Capturing the user's speech

    Once ESPHome device with a microphone detects the hot word, it will capture the user's speech, send it to Home Assistant.

3. it send audio.wav to  stt   

    When you speak to a ESPHome device with a microphone, it transcribes the audio from it into Speech-to-Text integration.Speech-to-Text service.

3. The Speech-to-Text integration is responsible for turning speech into text.
    The Speech-to-Text integration get the audio from it and send into Speech-to-Text service.
    The Speech-to-Text integration get  the result of turning speech into text.

4. The Conversation integration is responsible for processing user's text.The built-in conversation agent does this by matching it to an intent. 

5. The Intent integration is responsible for executing the intent and returning a response.

6. The Text-to-Speech integration is responsible for turning text into speech.

The Assist pipeline integration

The Assist pipeline integration runs the common steps of a voice assistant:
~~~
Wake word detection
Speech to text
Intent recognition
Text to speech
~~~
detail:https://developers.home-assistant.io/docs/voice/pipelines/



1. host - Run whisper on external server

hostname IP address:


I run faster_whisper with the medium-int8 model in a docker container on a vultr machine 

2. rpi
hostname IP address:
My HA core runs in docker-compose on a rpi.I’m running this and a few other containers on
Debian 12
rpi
1 GB RAM



3. Nabu Casa Home Assistant Voice Hardware 
hostname IP address:

## p

1. Found a suitable Whisper Container on Docker hub

wyoming-whisper docker image


which in theory runs the same command as the official add-on does.


## 

1. First,You simply run them as Wyoming services, with Docker

https://github.com/rhasspy/wyoming-piper

https://github.com/rhasspy/wyoming-faster-whisper




2. Second, you go to Settings > Integrations, add Wyoming Protocol. Then in Wyoming Protocol you click Add Service and point it to localhost port 10300 and then again with port 10400. 


3. Then under Voice Assistants you configure your pipeline to use them as STT and TTS.


## Step by Step

1. host

- installed docker on ubuntu

- I run faster_whisper with the medium-int8 model in a docker container on a vultr machine 

rhasspy/wyoming-whisper on vultr

whisper docker logs says it’s running fine:
Logs from whisper
~~~
INFO:__main__:Downloading FasterWhisperModel.TINY_INT8 to /data
INFO:__main__:Ready
~~~

Setting: --model tiny --language en → 6,09s almost instant response
Setting: --model base-int8 --language en → 6,79s short delay ~1s
Setting: --model base --language en → 7,69s delay ~2s

I followed this guide  to get it installed.

- Use wyoming piper TTS

2. Wyoming integration  to connect to the Whisper server

Then I add the wyoming integration in HA with the IP of my docker host 192.168.10.22 and 10300 port. It adds successfully.

which indicates that HA conatiner communicates with whisper server just fine.

wyoming piper and whisper are also working in HA (but offloaded to external server). everything works fine.



##  How to use

1. Exposing devices to assist
2. Exposing your entities to Assist
3. create an alias


Exposing devices to Voice assist
exposed entities to Voice assistant

Create aliases