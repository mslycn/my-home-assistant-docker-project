dns nameserver

# linux

# Optimize Your Home Assistant Database

Speed-up Home Assistant by reducing the database size

Speed-up Home Assistant by moving the database to memory

http://localhost:4999/boards/topic/13373/optimize-your-home-assistant-database


/var/lib/containerd




cpu 
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