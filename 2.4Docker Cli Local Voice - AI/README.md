## accuracy vs speed

background noise

accuracy - I tried the bigger model and accuracy better indeed. using the en medium-int8 model
speed - I think that being able to run whisper leveraging GPU 

## Note
wyoming-faster-whisper,如果没有英伟达显卡或未配置好CUDA环境，不要使用 large/large-v3 模型，可能导致内存耗尽死机.

## 
- Improve whisper performance on gpu hardware

CUDA 加速支持

- Improve whisper performance on intel hardware


# chapter 2 - Ubuntu with an NVidia GPU

if u dont have gpu it's slower, especially celeron is lower end cpu, u should use tiny.en model if unable to get powerful hardware.

For small models, it doesn't matter much because the speed differences are tiny. But for larger models (more accurate), a GPU can get done in milliseconds what takes a CPU several seconds.


## Improve whisper performance on hardware

通过Whisper的gpu模式来进行推理，模型选择medium，硬件要求是最低6G显存


Systems without an NVidia GPU

Ubuntu System with an NVidia GPU

Improving response times when using GPU


GPU

TPU

The only thing i had to do was to install the gpu drivers and nvidia container toolkit to the docker host and change the whisper image to a CUDA supporting one


Nvidia 显卡

先升级显卡驱动到最新，
然后去安装对应的 CUDA Toolkit 和 cudnn for CUDA11.X。



useful links

https://community.home-assistant.io/t/improve-whisper-performance-on-intel-hardware/699427/12

https://gloveboxes.github.io/OpenAI-Whisper-Transcriber-Sample/Whisper-Server/Whisper-Server-no-GPU/


费电是其次，因为大部分时间显卡都没有工作只有使用语音的是才会工作，一天工作不到30分钟。不使用的时候显卡大概6-9w功率。主要是显卡太贵了。3060我都是买的

