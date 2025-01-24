dns nameserver

# linux

# Optimize Your Home Assistant Database

Speed-up Home Assistant by reducing the database size

Speed-up Home Assistant by moving the database to memory

http://localhost:4999/boards/topic/13373/optimize-your-home-assistant-database


## Docker performance issues

实际上真正内存泄漏只有hass本身，因为本身hass就是docker;docker其实性能很低，无非是用的方便一些



http://localhost:4999/boards/topic/38181/ha-docker-dead-docker-performance-issues



## Optimize Your Home Assistant Docker

/var/lib/containerd


rpi p3b+

cpu 97.7%
~~~
docker pull ghcr.io/home-assistant/home-assistant:stable

~~~
output
~~~
top
top - 22:54:39 up 19 min,  2 users,  load average: 1.16, 0.58, 0.40
Tasks: 146 total,   1 running, 145 sleeping,   0 stopped,   0 zombie
%Cpu(s): 22.7 us, 10.3 sy,  0.0 ni, 52.4 id, 14.4 wa,  0.0 hi,  0.2 si,  0.0 st 
MiB Mem :    907.3 total,    120.5 free,    208.6 used,    638.8 buff/cache     
MiB Swap:    200.0 total,    151.7 free,     48.2 used.    698.7 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                      
    600 root      20   0 2011456  32380  14848 S  97.7   3.5   1:08.50 containerd                                   
   2491 root      20   0   28112   1536   1408 S  15.8   0.2   0:00.50 unpigz                                       
    699 root      20   0 2186024  59608  24064 S   5.0   6.4   0:36.57 dockerd                                      
     59 root      20   0       0      0      0 S   2.0   0.0   0:01.70 kswapd0                                      
     95 root      20   0       0      0      0 D   1.7   0.0   0:00.07 kworker/u11:1+flush-179:0                    
      1 root      20   0  168544   8932   6940 S   1.0   1.0   0:11.79 systemd                                      
   1291 root      20   0   19792   9016   7296 S   1.0   1.0   0:03.96 sshd                                         
   2321 root      20   0 1846340  27648  18304 S   1.0   3.0   0:01.45 docker                                       
   2438 pi        20   0   11712   4864   2816 R   1.0   0.5   0:00.15 top        


~~~


sudo git push -u origin main
~~~

cpu 100%
~~~
top
top - 22:42:51 up 7 min,  3 users,  load average: 0.58, 0.56, 0.35
Tasks: 151 total,   2 running, 149 sleeping,   0 stopped,   0 zombie
%Cpu(s): 26.0 us,  0.6 sy,  0.0 ni, 73.2 id,  0.1 wa,  0.0 hi,  0.2 si,  0.0 st 
MiB Mem :    907.3 total,    291.7 free,    350.2 used,    322.1 buff/cache     
MiB Swap:    200.0 total,    150.0 free,     50.0 used.    557.1 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                      
   1726 root      20   0  445176 171832   4636 R 100.0  18.5   0:27.94 git                                          
    710 nobody    20   0  723272  12560   5504 S   5.0   1.4   0:07.52 frpc                                         
   1527 root      20   0   11712   4864   2816 R   1.0   0.5   0:02.03 top                                          
    236 root      20   0   49956  12928  12288 S   0.3   1.4   0:02.22 systemd-journal                              
    474 avahi     20   0    7360   2944   2560 S   0.3   0.3   0:00.72 avahi-daemon                                 
   1621 root      20   0       0      0      0 I   0.3   0.0   0:00.01 kworker/u12:0-writeback                      
      1 root      20   0  168544   9316   7452 S   0.0   1.0   0:07.41 systemd     
~~~


docker restart ha

启动的初期cpu 100%，然后降低下来了
~~
top
top - 23:42:00 up 12 min,  2 users,  load average: 0.45, 1.18, 0.90
Tasks: 158 total,   1 running, 157 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.5 us,  0.4 sy,  0.0 ni, 93.8 id,  0.2 wa,  0.0 hi,  0.1 si,  0.0 st 
MiB Mem :    907.3 total,     62.9 free,    607.1 used,    293.9 buff/cache     
MiB Swap:    200.0 total,    165.9 free,     34.1 used.    300.3 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                      
   1712 root      20   0 1332392 485160  61056 S  19.9  52.2   2:08.12 python3                                      
    705 root      20   0 2111976  30540   8576 S   2.0   3.3   1:04.61 dockerd                                      
   1545 root      20   0       0      0      0 I   0.3   0.0   0:00.04 kworker/1:0-mm_percpu_wq                     
   1737 root      20   0   11712   4864   2816 R   0.3   0.5   0:02.97 top                      
~~