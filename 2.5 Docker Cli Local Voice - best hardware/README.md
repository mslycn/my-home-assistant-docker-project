# Home Assistant开源硬件语音助手设备

1. MIC在安静环境下收音距离
2. MIC在嘈杂环境下能否排除背景杂音（例如房间里在放电视）
3. 音箱在播放语音反馈的时候，用户能不能打断（例如：小爱音箱可以被新语音指令打断）


1. 
1个离线语音识别模块，用来做唤醒词。唤醒后，调用百度的识别接口识别内容，然后匹配本地预置的命令，再通过websocket发给ha

2. 
海凌科的语音模块,串口8266读取数据,然后http post到HA

3. 
用的海凌科的模块
只用它做唤醒词，唤醒一个Python的服务，后面就都是通过在线语音识别去搞
那个模块，唤醒的时候，串口会发一个消息。
用python写了个服务，监听串口的消息。当收到唤醒消息的时候，python就开始监听麦克风，后面的语音识别就是用python通过百度的语音识别接口做，不用海陵科的模块

4. 
用INMP441模块和ESP32可采集到声音，接下来就是与HASS的集成，怎么处理
打算用voice_assistant这个方案



OpenAI Whisper + ChatGPT


Home Assistant Cloud


Sherpa Onnx




【远程系列】HA Cloud登录流程分析 on wechat



