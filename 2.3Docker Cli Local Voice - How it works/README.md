
You can select Voice Assistant Pipeline for recognition process:
~~~
Speaker(audio)=>WAKE(wakeword addon) =>audio=> STT（whipser addon） =>Conversation=>Intent recognition=>action=>Intent execution=> NLP(text ,openai)=> TTS(result piper)
~~~
https://www.matterxiaomi.com/boards/topic/14594/voice-in-home-assistant#20849


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
