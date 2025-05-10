

## ha side
If it’s a problem with an integration or a memory leak changing hardware won’t save you.

ha side
See “sensor.memory_use” history if it’s rising gradually. If it’s not available enable it in system monitor.


## debian os side

Linux 死机日志：轻松排查系统故障问题 (linux 死机日志)

https://www.idc.net/help/142825/

在 Linux 中，系统日志分为多种，包括内核空间日志（Kernel Space Log）和用户空间日志（User Space Log）。内核空间日志是在操作系统内核运行过程中自动生成，包括了一个操作系统在运行期间发生的所有事件，包括各种软件和硬件交互、内存分配、 I/O 操作、驱动程序等操作。而用户空间日志则是用户程序或者应用在运行过程中所生成的日志信息。

在系统死机时，内核空间日志信息是非常重要的。因为内核空间日志记录了所有操作系统的运行信息，区别于用户空间日志仅包括用户程序运行时所生成的信息。内核空间日志记录的信息可以帮助开发者快速找到系统崩溃的原因。

内核空间日志一般存储在/var/log/kern.log 或者 /var/log/syslog。


在死机后重启系统后，系统会将之前存储在内存中的日志信息写入磁盘中。因此，我们可以在系统重新启动后通过以下命令来查看死机日志：

$ sudo dmesg -T

命令会输出最近的系统日志信息。如果系统在最近的时间发生了死机，则将包含有关此事件的详细信息。此外，您还可

 sudo cat /proc/cpuinfo
processor	: 0
BogoMIPS	: 38.40
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 1
BogoMIPS	: 38.40
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 2
BogoMIPS	: 38.40
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 3
BogoMIPS	: 38.40
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

Revision	: a22082
Serial		: 0000000018803c50
Model		: Raspberry Pi 3 Model B Rev 1.2

sudo cat /proc/meminfo

 cat /proc/meminfo
MemTotal:         929104 kB
MemFree:           27236 kB
MemAvailable:     234840 kB
Buffers:          132868 kB
Cached:           100748 kB
SwapCached:         1828 kB
Active:           305192 kB
Inactive:         490708 kB
Active(anon):     276000 kB
Inactive(anon):   284916 kB
Active(file):      29192 kB
Inactive(file):   205792 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:        204796 kB
SwapFree:          28916 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:              1416 kB
Writeback:             0 kB
AnonPages:        560492 kB
Mapped:            65324 kB
Shmem:                12 kB
KReclaimable:      35608 kB
Slab:              60644 kB
SReclaimable:      35608 kB
SUnreclaim:        25036 kB
KernelStack:        4288 kB
PageTables:         5652 kB
SecPageTables:         0 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:      669348 kB
Committed_AS:    1366660 kB
VmallocTotal:   257687552 kB
VmallocUsed:       12856 kB
VmallocChunk:          0 kB
Percpu:              720 kB
CmaTotal:         262144 kB
CmaFree:              16 kB


在查看日志信息时，需要注意日志输出的时间戳。在解读日志时，您需要首先标识出问题开始的时间，以此为起点进行分析。同时，需要了解以下一些关键信息：

• CPU、内核和操作系统版本信息

• 硬件设备信息，如NIC、SCSI和RD控制器，以及其他驱动程序

• 内存使用情况和负载

• 各种进程的启动和停止时间

• 系统的启动和停止时间

• 错误处理和其他通知

通过这些信息，您可以更快地查找问题并排除故障。




/var/log/kern.log 是 Ubuntu 和 Debian 系统的系统日志文件；而 /var/log/syslog 是 Red Hat 系统的系统日志文件。

~# journalctl
Mar 09 01:19:55 raspberrypi restart-frpc.sh[693]: frpc is  running...
Mar 09 01:19:56 raspberrypi systemd-journald[234]: /var/log/journal/68d88383280a4bfab87fcd319795a88a/system.journal:>
Mar 09 01:19:56 raspberrypi systemd-journald[234]: Failed to write entry to /var/log/journal/68d88383280a4bfab87fcd3>
Mar 09 01:19:56 raspberrypi systemd-journald[234]: Failed to create new system journal: No such file or directory
Mar 09 01:20:00 raspberrypi restart-frpc.sh[693]: frpc is  running...


# journalctl -p err
Mar 09 01:19:56 raspberrypi systemd-journald[234]: Failed to create new system journal: No such file or directory
Mar 09 01:39:12 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 01:45:15 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 01:53:19 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 02:01:25 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 02:03:26 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 02:07:28 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 02:11:30 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 02:17:32 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 02:23:35 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 02:25:36 raspberrypi kernel: hwmon hwmon1: Undervoltage detected!
Mar 09 02:27:37 raspberrypi k

- 查看过去Linux操作系统的重启日志
last | grep reboot
reboot   system boot  6.6.20+rpt-rpi-v Tue Mar 11 13:17   still running
reboot   system boot  6.6.20+rpt-rpi-v Fri Mar  7 17:16   still running
reboot   system boot  6.6.20+rpt-rpi-v Wed Mar  5 09:16   still running
reboot   system boot  6.6.20+rpt-rpi-v Mon Mar  3 04:17   still running


journalctl --since "2025-3-11 13:00:00" --until "2025-3-11 13:17:00"



du -h /var/log --max-depth=1 | sort -hr | head -n 10

journalctl --vacuum-size=10M



du -ha /var/lib/docker/containers/ | grep "json.log" | sort -rh

truncate -s 0 /var/lib/docker/containers/*/*-json.log 



https://ivanzz1001.github.io/records/post/linuxops/2018/04/10/linux-restart-log  ok


log
1.修复全部出错自动化

