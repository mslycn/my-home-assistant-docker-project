accuracy 

speed

background noise

accuracy - I tried the bigger model and accuracy better indeed. using the en medium-int8 model
speed - I think that being able to run whisper leveraging GPU 




Improve whisper performance on gpu hardware


Improve whisper performance on intel hardware


# chapter 2 - Ubuntu with an NVidia GPU

if u dont have gpu it's slower, especially celeron is lower end cpu, u should use tiny.en model if unable to get powerful hardware.

For small models, it doesn't matter much because the speed differences are tiny. But for larger models (more accurate), a GPU can get done in milliseconds what takes a CPU several seconds.


## Improve whisper performance on hardware




Systems without an NVidia GPU

Ubuntu with an NVidia GPU

Improving response times when using GPU


GPU

TPU

The only thing i had to do was to install the gpu drivers and nvidia container toolkit to the docker host and change the whisper image to a CUDA supporting one

useful links

https://community.home-assistant.io/t/improve-whisper-performance-on-intel-hardware/699427/12

https://gloveboxes.github.io/OpenAI-Whisper-Transcriber-Sample/Whisper-Server/Whisper-Server-no-GPU/

