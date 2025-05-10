## Hardware Setup
~~~
Install Raspberry https://www.raspberrypi.com/software/
Burn the image to an SD card
Boot the Raspberry Pi
Connect to the Raspberry Pi via xshell
Open a terminal
~~~

## OS information

Debian is the only officially supported Linux distro for use with Home Assistant.

operating system

cat /etc/os-release

~~~
PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
NAME="Debian GNU/Linux"
VERSION_ID="12"
VERSION="12 (bookworm)"
VERSION_CODENAME=bookworm
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"


~~~

print information about the running distribution

lsb_release -a 
~~~
No LSB modules are available.
Distributor ID:	Debian
Description:	Debian GNU/Linux 12 (bookworm)
Release:	12
Codename:	bookworm
~~~

subversion IDs for Debian

cat /etc/debian_version
~~~
12.7

~~~


cat /proc/version
~~~
Linux version 6.6.20+rpt-rpi-v8 (debian-kernel@lists.debian.org) (gcc-12 (Debian 12.2.0-14) 12.2.0, GNU ld (GNU Binutils for Debian) 2.40) #1 SMP PREEMPT Debian 1:6.6.20-1+rpt1 (2024-03-07)
~~~

Kernel version

uname -r
~~~
6.6.20+rpt-rpi-v8
~~~

cat /etc/issue 
~~~
Debian GNU/Linux 12 \n \l
~~~

Is your Raspberry Pi running a 64 or 32 bits OS?
~~~
uname -m
~~~

## sudo nano /etc/apt/sources.list

cat /etc/apt/sources.list.d/raspi.list
~~~
cat /etc/apt/sources.list.d/raspi.list
deb http://archive.raspberrypi.com/debian/ bookworm main
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://archive.raspberrypi.com/debian/ bookworm main
~~~


## set static ip address

How to Configure Static IP Address on Debian 12

使用nmcli设置静态IPv4地址

nmcli con show
~~~
NAME                UUID                                  TYPE      DEVICE          
Wired connection 1  33d44833-54da-3fa3-9a4c-0357e50c6c34  ethernet  eth0            
lo                  481d0abe-4586-4287-87bc-69cadce3a63d  loopback  lo              
br-424eb587074d     5632186d-34b6-4d73-a45b-80583dbac37a  bridge    br-424eb587074d 
docker0             53271779-f1f5-4908-add4-c38a91a90f90  bridge    docker0  
~~~



https://blog.csdn.net/gongchenyu/article/details/134675480





