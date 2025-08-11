Offcial website：
https://www.music-assistant.io/



docker pull ghcr.io/music-assistant/server:latest    arm64

docker run -v <dir>:/data --network host --cap-add=DAC_READ_SEARCH --cap-add=SYS_ADMIN --security-opt apparmor:unconfined ghcr.io/music-assistant/server

docker run -v /datadocker/music-assistant:/data --network host --cap-add=DAC_READ_SEARCH --cap-add=SYS_ADMIN --security-opt apparmor:unconfined ghcr.io/music-assistant/server

8095


fourm

http://localhost:4999/boards/topic/43287/music-assistant-server-project-for-home-assistant

blog

https://blog.matterxiaomi.com/blog/Multi-room-audio-Home-Assistant-part1/





