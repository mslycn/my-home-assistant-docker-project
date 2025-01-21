docker images

~~~
REPOSITORY                TAG       IMAGE ID       CREATED      SIZE
ghcr.io/esphome/esphome   latest    13cc1ca1d6e6   4 days ago   643MB
ghcr.io/esphome/esphome   stable    13cc1ca1d6e6   4 days ago   643MB
~~~
解释：
~~~
REPOSITORY: 来自于哪个仓库；
TAG: 镜像的标签信息，比如 5.7、latest 表示不同的版本信息；
IMAGE ID: 镜像的 ID, 如果您看到两个 ID 完全相同，那么实际上，它们指向的是同一个镜像，只是标签名称不同罢了；如：allen_mysql:5.7 和 docker.io/mysql:5.7 的镜像 ID 是一模一样的，说明它们是同一个镜像，只是别名不同而已。
CREATED: 镜像最后的更新时间；
SIZE: 镜像的大小
~~~


## docker run 

docker system df
~~~
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          1         1         643.3MB   0B (0%)
Containers      1         1         745.5kB   0B (0%)
Local Volumes   0         0         0B        0B
Build Cache     0         0         0B        0B

~~~

docker system df -v 
~~~
Images space usage:

REPOSITORY                TAG       IMAGE ID       CREATED      SIZE      SHARED SIZE   UNIQUE SIZE   CONTAINERS
ghcr.io/esphome/esphome   latest    13cc1ca1d6e6   4 days ago   643MB     0B            643.3MB       1

Containers space usage:

CONTAINER ID   IMAGE                     COMMAND                  LOCAL VOLUMES   SIZE      CREATED          STATUS                    NAMES
cca698afb677   ghcr.io/esphome/esphome   "/entrypoint.sh dash…"   0               746kB     14 minutes ago   Up 14 minutes (healthy)   esphome

Local Volumes space usage:

VOLUME NAME   LINKS     SIZE

Build cache usage: 0B

CACHE ID   CACHE TYPE   SIZE      CREATED   LAST USED   USAGE     SHARED

~~~

## tree


sudo tree /var/lib/containerd -L 5

~~~
/var/lib/containerd
├── io.containerd.content.v1.content
│   ├── blobs
│   │   └── sha256
│   │       ├── 9874fb1af9aac33595881c9ae3b6caa3a6424a09589f3f35368da54abfde7fa6
│   │       └── be49fcab700d25f56db6b27069036469a717a304219a914b484971b8889fdace
│   └── ingest
├── io.containerd.metadata.v1.bolt
│   └── meta.db
├── io.containerd.runtime.v1.linux
├── io.containerd.runtime.v2.task
│   └── moby
│       └── cca698afb6776bb6b5fca18c2b8fe2672864df5d7dd44b3edd8c4d3f65dbbaaa
├── io.containerd.snapshotter.v1.blockfile
├── io.containerd.snapshotter.v1.btrfs
├── io.containerd.snapshotter.v1.native
│   └── snapshots
├── io.containerd.snapshotter.v1.overlayfs
│   └── snapshots
└── tmpmounts

17 directories, 3 files



~~~

## disk 

sudo du -h --max-depth=1 /var/lib/containerd | sort -hr
~~
172K	/var/lib/containerd
100K	/var/lib/containerd/io.containerd.metadata.v1.bolt
24K	/var/lib/containerd/io.containerd.content.v1.content
12K	/var/lib/containerd/io.containerd.runtime.v2.task
8.0K	/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs
8.0K	/var/lib/containerd/io.containerd.snapshotter.v1.native
4.0K	/var/lib/containerd/tmpmounts
4.0K	/var/lib/containerd/io.containerd.snapshotter.v1.btrfs
4.0K	/var/lib/containerd/io.containerd.snapshotter.v1.blockfile
4.0K	/var/lib/containerd/io.containerd.runtime.v1.linux


~~


## tree



tree /var/lib/docker -L 5

~~~
/var/lib/docker
├── buildkit
│   ├── cache.db
│   ├── containerdmeta.db
│   ├── executor
│   ├── history.db
│   ├── metadata_v2.db
│   └── snapshots.db
├── containers
│   └── cca698afb6776bb6b5fca18c2b8fe2672864df5d7dd44b3edd8c4d3f65dbbaaa
│       ├── cca698afb6776bb6b5fca18c2b8fe2672864df5d7dd44b3edd8c4d3f65dbbaaa-json.log
│       ├── checkpoints
│       ├── config.v2.json
│       ├── hostconfig.json
│       ├── hostname
│       ├── hosts
│       ├── mounts
│       ├── resolv.conf
│       └── resolv.conf.hash
├── engine-id
├── image
│   └── overlay2
│       ├── distribution
│       │   ├── diffid-by-digest
│       │   │   └── sha256
│       │   └── v2metadata-by-diffid
│       │       └── sha256
│       ├── imagedb
│       │   ├── content
│       │   │   └── sha256
│       │   └── metadata
│       │       └── sha256
│       ├── layerdb
│       │   ├── mounts
│       │   │   └── cca698afb6776bb6b5fca18c2b8fe2672864df5d7dd44b3edd8c4d3f65dbbaaa
│       │   ├── sha256
│       │   │   ├── 0d3792763fe1f4988e8b525af130280e9ba425ad90e0f861c1e723a1d9c1c792
│       │   │   ├── 0eeb7800a610ebfeb9f6dcd5ef3df45bcdc415fe61dc594243b36f6098520d07
│       │   │   ├── 129a0e2d847c676609f2725f781006a68deb9f0a0e611f303f1c30c1c6920741
│       │   │   ├── 18fd61eea0efcc81218b036ca9158e690e23a9d345c9c5759be46016ec2be442
│       │   │   ├── 1bf61a92fd79a2e20705224424cba611c10de877ea6ef30ccf7baa822cf88e82
│       │   │   ├── 4eb12c4bf7604f553c294039fedba379744c5ae1e11377a2c865d8510f48ec9f
│       │   │   ├── 78e44c3f29acb5c7e41ff90a9314a2a061f30685c2c414c44d09da9d67a38bfd
│       │   │   ├── 8d7935af6a0d6c6ba95ca36b997193a405b3decc8ec4f3811ab688272d877857
│       │   │   ├── 92770f546e065c4942829b1f0d7d1f02c2eb1e6acf0d1bc08ef0bf6be4972839
│       │   │   ├── a8de6cdcd07677ea83fcf3fe4a448f8adf6135dd7746843b97b8a2d5260ec32e
│       │   │   ├── b47dd77d5e2de2126f13fe612156bddd4d4b9f7fd10d2d4ef7ca8d7a63b48410
│       │   │   ├── cffc1955ecdf93c8b67836af263d3c6212be2899f4482bf53b2f59e93df7a8f9
│       │   │   └── fe55a0c59f3d70fc62f9a6caa746a07cfefcba7315200e67ca34974dd3731182
│       │   └── tmp
│       └── repositories.json
├── network
│   └── files
│       └── local-kv.db
├── overlay2
│   ├── 5524a71997ac535549f76d546933e43fd2d440742412a61729dfddef6a15237a
│   │   ├── committed
│   │   ├── diff
│   │   │   └── etc
│   │   │       └── gitconfig
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── 69ac9ccf03bb68ff25cf783af1eec6eec2a193d512cb4c3f6ab6f846c9656d2d
│   │   ├── committed
│   │   ├── diff
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── 741b9e6aab4e1a4a13297fe1a41bcf6c69d84c7890bfa20d0c4bea1525bee279
│   │   ├── committed
│   │   ├── diff
│   │   │   ├── etc
│   │   │   │   ├── bash_completion.d
│   │   │   │   ├── ca-certificates
│   │   │   │   ├── ca-certificates.conf
│   │   │   │   ├── fonts
│   │   │   │   ├── group
│   │   │   │   ├── group-
│   │   │   │   ├── gshadow
│   │   │   │   ├── gshadow-
│   │   │   │   ├── gss
│   │   │   │   ├── inputrc
│   │   │   │   ├── ld.so.cache
│   │   │   │   ├── magic
│   │   │   │   ├── magic.mime
│   │   │   │   ├── mime.types
│   │   │   │   ├── netconfig
│   │   │   │   ├── perl
│   │   │   │   ├── python3
│   │   │   │   ├── python3.11
│   │   │   │   ├── ssh
│   │   │   │   └── ssl
│   │   │   ├── run
│   │   │   │   └── adduser
│   │   │   ├── usr
│   │   │   │   ├── bin
│   │   │   │   ├── lib
│   │   │   │   ├── local
│   │   │   │   ├── sbin
│   │   │   │   └── share
│   │   │   └── var
│   │   │       ├── cache
│   │   │       ├── lib
│   │   │       └── log
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── 7c40e04839cab302367a3899eda693bc825a67cf435f66d71e1bd85df7a23aca
│   │   ├── committed
│   │   ├── diff
│   │   │   ├── bin -> usr/bin
│   │   │   ├── boot
│   │   │   ├── dev
│   │   │   ├── etc
│   │   │   │   ├── adduser.conf
│   │   │   │   ├── alternatives
│   │   │   │   ├── apt
│   │   │   │   ├── bash.bashrc
│   │   │   │   ├── bindresvport.blacklist
│   │   │   │   ├── cron.d
│   │   │   │   ├── cron.daily
│   │   │   │   ├── debconf.conf
│   │   │   │   ├── debian_version
│   │   │   │   ├── default
│   │   │   │   ├── deluser.conf
│   │   │   │   ├── dpkg
│   │   │   │   ├── e2scrub.conf
│   │   │   │   ├── environment
│   │   │   │   ├── fstab
│   │   │   │   ├── gai.conf
│   │   │   │   ├── group
│   │   │   │   ├── group-
│   │   │   │   ├── gshadow
│   │   │   │   ├── host.conf
│   │   │   │   ├── hostname
│   │   │   │   ├── init.d
│   │   │   │   ├── issue
│   │   │   │   ├── issue.net
│   │   │   │   ├── kernel
│   │   │   │   ├── ld.so.cache
│   │   │   │   ├── ld.so.conf
│   │   │   │   ├── ld.so.conf.d
│   │   │   │   ├── libaudit.conf
│   │   │   │   ├── localtime -> /usr/share/zoneinfo/Etc/UTC
│   │   │   │   ├── login.defs
│   │   │   │   ├── logrotate.d
│   │   │   │   ├── mke2fs.conf
│   │   │   │   ├── motd
│   │   │   │   ├── nsswitch.conf
│   │   │   │   ├── opt
│   │   │   │   ├── os-release -> ../usr/lib/os-release
│   │   │   │   ├── pam.conf
│   │   │   │   ├── pam.d
│   │   │   │   ├── passwd
│   │   │   │   ├── passwd-
│   │   │   │   ├── profile
│   │   │   │   ├── profile.d
│   │   │   │   ├── rc0.d
│   │   │   │   ├── rc1.d
│   │   │   │   ├── rc2.d
│   │   │   │   ├── rc3.d
│   │   │   │   ├── rc4.d
│   │   │   │   ├── rc5.d
│   │   │   │   ├── rc6.d
│   │   │   │   ├── rcS.d
│   │   │   │   ├── resolv.conf
│   │   │   │   ├── rmt -> /usr/sbin/rmt
│   │   │   │   ├── security
│   │   │   │   ├── selinux
│   │   │   │   ├── shadow
│   │   │   │   ├── shells
│   │   │   │   ├── skel
│   │   │   │   ├── subgid
│   │   │   │   ├── subuid
│   │   │   │   ├── systemd
│   │   │   │   ├── terminfo
│   │   │   │   ├── timezone
│   │   │   │   ├── update-motd.d
│   │   │   │   └── xattr.conf
│   │   │   ├── home
│   │   │   ├── lib -> usr/lib
│   │   │   ├── lib32 -> usr/lib32
│   │   │   ├── lib64 -> usr/lib64
│   │   │   ├── libx32 -> usr/libx32
│   │   │   ├── media
│   │   │   ├── mnt
│   │   │   ├── opt
│   │   │   ├── proc
│   │   │   ├── root
│   │   │   ├── run
│   │   │   │   └── lock
│   │   │   ├── sbin -> usr/sbin
│   │   │   ├── srv
│   │   │   ├── sys
│   │   │   ├── tmp
│   │   │   ├── usr
│   │   │   │   ├── bin
│   │   │   │   ├── games
│   │   │   │   ├── include
│   │   │   │   ├── lib
│   │   │   │   ├── lib32
│   │   │   │   ├── lib64
│   │   │   │   ├── libexec
│   │   │   │   ├── libx32
│   │   │   │   ├── local
│   │   │   │   ├── sbin
│   │   │   │   ├── share
│   │   │   │   └── src
│   │   │   └── var
│   │   │       ├── backups
│   │   │       ├── cache
│   │   │       ├── lib
│   │   │       ├── local
│   │   │       ├── lock -> /run/lock
│   │   │       ├── log
│   │   │       ├── mail
│   │   │       ├── opt
│   │   │       ├── run -> /run
│   │   │       ├── spool
│   │   │       └── tmp
│   │   └── link
│   ├── 815272d24e15f18b93f0d881f1fd47e6253a7463f5b7dcb6e08392769e3cd7fe
│   │   ├── diff
│   │   │   └── esphome
│   │   │       └── esphome
│   │   ├── link
│   │   ├── lower
│   │   ├── merged
│   │   │   ├── bin -> usr/bin
│   │   │   ├── boot
│   │   │   ├── config
│   │   │   ├── dev
│   │   │   │   ├── console
│   │   │   │   ├── pts
│   │   │   │   └── shm
│   │   │   ├── entrypoint.sh
│   │   │   ├── esphome
│   │   │   │   ├── CODE_OF_CONDUCT.md
│   │   │   │   ├── CODEOWNERS
│   │   │   │   ├── CONTRIBUTING.md
│   │   │   │   ├── docker
│   │   │   │   ├── esphome
│   │   │   │   ├── esphome.egg-info
│   │   │   │   ├── LICENSE
│   │   │   │   ├── MANIFEST.in
│   │   │   │   ├── platformio.ini
│   │   │   │   ├── pyproject.toml
│   │   │   │   ├── README.md
│   │   │   │   ├── requirements_dev.txt
│   │   │   │   ├── requirements_optional.txt
│   │   │   │   ├── requirements_test.txt
│   │   │   │   ├── requirements.txt
│   │   │   │   ├── script
│   │   │   │   ├── sdkconfig.defaults
│   │   │   │   └── tests
│   │   │   ├── etc
│   │   │   │   ├── adduser.conf
│   │   │   │   ├── alternatives
│   │   │   │   ├── apt
│   │   │   │   ├── bash.bashrc
│   │   │   │   ├── bash_completion.d
│   │   │   │   ├── bindresvport.blacklist
│   │   │   │   ├── ca-certificates
│   │   │   │   ├── ca-certificates.conf
│   │   │   │   ├── cron.d
│   │   │   │   ├── cron.daily
│   │   │   │   ├── debconf.conf
│   │   │   │   ├── debian_version
│   │   │   │   ├── default
│   │   │   │   ├── deluser.conf
│   │   │   │   ├── dpkg
│   │   │   │   ├── e2scrub.conf
│   │   │   │   ├── environment
│   │   │   │   ├── fonts
│   │   │   │   ├── fstab
│   │   │   │   ├── gai.conf
│   │   │   │   ├── gitconfig
│   │   │   │   ├── group
│   │   │   │   ├── group-
│   │   │   │   ├── gshadow
│   │   │   │   ├── gshadow-
│   │   │   │   ├── gss
│   │   │   │   ├── host.conf
│   │   │   │   ├── hostname
│   │   │   │   ├── hosts
│   │   │   │   ├── init.d
│   │   │   │   ├── inputrc
│   │   │   │   ├── issue
│   │   │   │   ├── issue.net
│   │   │   │   ├── kernel
│   │   │   │   ├── ld.so.cache
│   │   │   │   ├── ld.so.conf
│   │   │   │   ├── ld.so.conf.d
│   │   │   │   ├── libaudit.conf
│   │   │   │   ├── localtime -> /usr/share/zoneinfo/Etc/UTC
│   │   │   │   ├── login.defs
│   │   │   │   ├── logrotate.d
│   │   │   │   ├── magic
│   │   │   │   ├── magic.mime
│   │   │   │   ├── mime.types
│   │   │   │   ├── mke2fs.conf
│   │   │   │   ├── motd
│   │   │   │   ├── mtab -> /proc/mounts
│   │   │   │   ├── netconfig
│   │   │   │   ├── nsswitch.conf
│   │   │   │   ├── opt
│   │   │   │   ├── os-release -> ../usr/lib/os-release
│   │   │   │   ├── pam.conf
│   │   │   │   ├── pam.d
│   │   │   │   ├── passwd
│   │   │   │   ├── passwd-
│   │   │   │   ├── perl
│   │   │   │   ├── profile
│   │   │   │   ├── profile.d
│   │   │   │   ├── python3
│   │   │   │   ├── python3.11
│   │   │   │   ├── rc0.d
│   │   │   │   ├── rc1.d
│   │   │   │   ├── rc2.d
│   │   │   │   ├── rc3.d
│   │   │   │   ├── rc4.d
│   │   │   │   ├── rc5.d
│   │   │   │   ├── rc6.d
│   │   │   │   ├── rcS.d
│   │   │   │   ├── resolv.conf
│   │   │   │   ├── rmt -> /usr/sbin/rmt
│   │   │   │   ├── security
│   │   │   │   ├── selinux
│   │   │   │   ├── shadow
│   │   │   │   ├── shells
│   │   │   │   ├── skel
│   │   │   │   ├── ssh
│   │   │   │   ├── ssl
│   │   │   │   ├── subgid
│   │   │   │   ├── subuid
│   │   │   │   ├── systemd
│   │   │   │   ├── terminfo
│   │   │   │   ├── timezone
│   │   │   │   ├── update-motd.d
│   │   │   │   └── xattr.conf
│   │   │   ├── home
│   │   │   ├── lib -> usr/lib
│   │   │   ├── lib32 -> usr/lib32
│   │   │   ├── lib64 -> usr/lib64
│   │   │   ├── libx32 -> usr/libx32
│   │   │   ├── media
│   │   │   ├── mnt
│   │   │   ├── opt
│   │   │   ├── piolibs
│   │   │   │   ├── ArduinoJson
│   │   │   │   ├── arduino-MLX90393
│   │   │   │   ├── AsyncMqttClient-esphome
│   │   │   │   ├── AsyncTCP-esphome
│   │   │   │   ├── AsyncTCP-esphome@1.2.2
│   │   │   │   ├── Crypto
│   │   │   │   ├── Dsmr
│   │   │   │   ├── ESP32-audioI2S
│   │   │   │   ├── ESPAsyncTCP-esphome
│   │   │   │   ├── ESPAsyncWebServer-esphome
│   │   │   │   ├── esp_mbedtls_esp8266
│   │   │   │   ├── ESPMicroSpeechFeatures
│   │   │   │   ├── esp_wireguard
│   │   │   │   ├── FastLED
│   │   │   │   ├── HaierProtocol
│   │   │   │   ├── HeatpumpIR
│   │   │   │   ├── Improv
│   │   │   │   ├── IRremoteESP8266
│   │   │   │   ├── libsodium
│   │   │   │   ├── lvgl
│   │   │   │   ├── MideaUART
│   │   │   │   ├── NeoPixelBus
│   │   │   │   ├── noise-c
│   │   │   │   ├── noise-c@0.1.1
│   │   │   │   ├── pngle
│   │   │   │   ├── qr-code-generator-library
│   │   │   │   ├── TinyGPSPlus
│   │   │   │   └── TM1651
│   │   │   ├── platformio.ini
│   │   │   ├── platformio_install_deps.py
│   │   │   ├── proc
│   │   │   ├── requirements_optional.txt
│   │   │   ├── requirements.txt
│   │   │   ├── root
│   │   │   ├── run
│   │   │   │   ├── adduser
│   │   │   │   └── lock
│   │   │   ├── sbin -> usr/sbin
│   │   │   ├── srv
│   │   │   ├── sys
│   │   │   ├── tmp
│   │   │   ├── usr
│   │   │   │   ├── bin
│   │   │   │   ├── games
│   │   │   │   ├── include
│   │   │   │   ├── lib
│   │   │   │   ├── lib32
│   │   │   │   ├── lib64
│   │   │   │   ├── libexec
│   │   │   │   ├── libx32
│   │   │   │   ├── local
│   │   │   │   ├── sbin
│   │   │   │   ├── share
│   │   │   │   └── src
│   │   │   └── var
│   │   │       ├── backups
│   │   │       ├── cache
│   │   │       ├── lib
│   │   │       ├── local
│   │   │       ├── lock -> /run/lock
│   │   │       ├── log
│   │   │       ├── mail
│   │   │       ├── opt
│   │   │       ├── run -> /run
│   │   │       ├── spool
│   │   │       └── tmp
│   │   └── work
│   │       └── work
│   ├── 815272d24e15f18b93f0d881f1fd47e6253a7463f5b7dcb6e08392769e3cd7fe-init
│   │   ├── committed
│   │   ├── diff
│   │   │   ├── dev
│   │   │   │   ├── console
│   │   │   │   ├── pts
│   │   │   │   └── shm
│   │   │   └── etc
│   │   │       ├── hostname
│   │   │       ├── hosts
│   │   │       ├── mtab -> /proc/mounts
│   │   │       └── resolv.conf
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   │       └── work
│   │           └── #c
│   ├── 9606b0a13b76fccedf4a3dad6ad3cb508fec2fddcc1d93ba11b60919d2783460
│   │   ├── committed
│   │   ├── diff
│   │   │   ├── piolibs
│   │   │   │   ├── ArduinoJson
│   │   │   │   ├── arduino-MLX90393
│   │   │   │   ├── AsyncMqttClient-esphome
│   │   │   │   ├── AsyncTCP-esphome
│   │   │   │   ├── AsyncTCP-esphome@1.2.2
│   │   │   │   ├── Crypto
│   │   │   │   ├── Dsmr
│   │   │   │   ├── ESP32-audioI2S
│   │   │   │   ├── ESPAsyncTCP-esphome
│   │   │   │   ├── ESPAsyncWebServer-esphome
│   │   │   │   ├── esp_mbedtls_esp8266
│   │   │   │   ├── ESPMicroSpeechFeatures
│   │   │   │   ├── esp_wireguard
│   │   │   │   ├── FastLED
│   │   │   │   ├── HaierProtocol
│   │   │   │   ├── HeatpumpIR
│   │   │   │   ├── Improv
│   │   │   │   ├── IRremoteESP8266
│   │   │   │   ├── libsodium
│   │   │   │   ├── lvgl
│   │   │   │   ├── MideaUART
│   │   │   │   ├── NeoPixelBus
│   │   │   │   ├── noise-c
│   │   │   │   ├── noise-c@0.1.1
│   │   │   │   ├── pngle
│   │   │   │   ├── qr-code-generator-library
│   │   │   │   ├── TinyGPSPlus
│   │   │   │   └── TM1651
│   │   │   └── root
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── 97f4237e056509140d8b0cc729f72b060b258517d41ce4e13d6cc90135956738
│   │   ├── committed
│   │   ├── diff
│   │   │   └── usr
│   │   │       └── local
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── a68ba3ad1e7d8e8b3a9a21bcad7b55065ceb1831d42ef1bdd7d71d5d1031569f
│   │   ├── committed
│   │   ├── diff
│   │   │   └── esphome
│   │   │       ├── CODE_OF_CONDUCT.md
│   │   │       ├── CODEOWNERS
│   │   │       ├── CONTRIBUTING.md
│   │   │       ├── docker
│   │   │       ├── esphome
│   │   │       ├── LICENSE
│   │   │       ├── MANIFEST.in
│   │   │       ├── platformio.ini
│   │   │       ├── pyproject.toml
│   │   │       ├── README.md
│   │   │       ├── requirements_dev.txt
│   │   │       ├── requirements_optional.txt
│   │   │       ├── requirements_test.txt
│   │   │       ├── requirements.txt
│   │   │       ├── script
│   │   │       ├── sdkconfig.defaults
│   │   │       └── tests
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── b95be3c703ee775067087390c948b4906206d3867cbdde9c606354eeda91f90f
│   │   ├── committed
│   │   ├── diff
│   │   │   ├── platformio.ini
│   │   │   └── platformio_install_deps.py
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── bfd34125132b2bd634ea2475e38703bd30ae5e6ae2c22fec0cde7554d8c5b5cc
│   │   ├── committed
│   │   ├── diff
│   │   │   ├── esphome
│   │   │   │   └── esphome.egg-info
│   │   │   ├── root
│   │   │   └── usr
│   │   │       └── local
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── c2a415384e1eae58954330c002bb41a86410e7b0010a0122bbe5b01078566ce4
│   │   ├── committed
│   │   ├── diff
│   │   │   └── entrypoint.sh
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── db5ca272df9bc82e135306415fae877a2da32ac3f8c18af4330a550e19c73e3c
│   │   ├── committed
│   │   ├── diff
│   │   │   ├── piolibs
│   │   │   ├── root
│   │   │   └── usr
│   │   │       └── local
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── e007061cd51f7b45dc6ca462d2b3d36aa75a29122a0bea6d7f9414852e3023f5
│   │   ├── committed
│   │   ├── diff
│   │   │   └── config
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   ├── fbd8d58b054f845016f88ee82983693229eaf463d4f1af03472bf023a08e3f22
│   │   ├── committed
│   │   ├── diff
│   │   │   ├── requirements_optional.txt
│   │   │   └── requirements.txt
│   │   ├── link
│   │   ├── lower
│   │   └── work
│   └── l
│       ├── 2NRK4VFVKE45NF27W3CVWVHRHG -> ../815272d24e15f18b93f0d881f1fd47e6253a7463f5b7dcb6e08392769e3cd7fe/diff
│       ├── 3QFUIEQ67PUYPEBBQTEJASO62K -> ../9606b0a13b76fccedf4a3dad6ad3cb508fec2fddcc1d93ba11b60919d2783460/diff
│       ├── 4H6L4Y2IB7IEY6CNPHR6GJJ6T4 -> ../a68ba3ad1e7d8e8b3a9a21bcad7b55065ceb1831d42ef1bdd7d71d5d1031569f/diff
│       ├── D3YWZ272LBI4EITH3QSOOLLS7Y -> ../741b9e6aab4e1a4a13297fe1a41bcf6c69d84c7890bfa20d0c4bea1525bee279/diff
│       ├── E4JZETNCPRSIHDANVW6AYBFHYJ -> ../c2a415384e1eae58954330c002bb41a86410e7b0010a0122bbe5b01078566ce4/diff
│       ├── ESTNIDMQ5CTYECVQ24K3RUENPF -> ../fbd8d58b054f845016f88ee82983693229eaf463d4f1af03472bf023a08e3f22/diff
│       ├── FNK6MKIRYDFIELOZEDNN73PPDD -> ../db5ca272df9bc82e135306415fae877a2da32ac3f8c18af4330a550e19c73e3c/diff
│       ├── FVZOILHD5CKXWHC5XBCRGVMYRT -> ../815272d24e15f18b93f0d881f1fd47e6253a7463f5b7dcb6e08392769e3cd7fe-init/diff
│       ├── KUNWJTPZFFVFYCAFVPS4VIQCVX -> ../e007061cd51f7b45dc6ca462d2b3d36aa75a29122a0bea6d7f9414852e3023f5/diff
│       ├── O4DBQUBGLZXJD2RHKK3RYAD3M4 -> ../69ac9ccf03bb68ff25cf783af1eec6eec2a193d512cb4c3f6ab6f846c9656d2d/diff
│       ├── PQYJLD6ACM5FKRHFOB2ZCPRT33 -> ../b95be3c703ee775067087390c948b4906206d3867cbdde9c606354eeda91f90f/diff
│       ├── QDEDRISDNXQJL7PCWQ6RZS7IKN -> ../97f4237e056509140d8b0cc729f72b060b258517d41ce4e13d6cc90135956738/diff
│       ├── RZL6X6PIZ2OBEO3YQ6QFAME37Z -> ../7c40e04839cab302367a3899eda693bc825a67cf435f66d71e1bd85df7a23aca/diff
│       ├── UQ6HLZSVYUQLJOUWNBW35KR7M3 -> ../5524a71997ac535549f76d546933e43fd2d440742412a61729dfddef6a15237a/diff
│       └── XSUSJIAUYOS7RAO2XDSPILQO7Y -> ../bfd34125132b2bd634ea2475e38703bd30ae5e6ae2c22fec0cde7554d8c5b5cc/diff
├── plugins
│   └── tmp
├── runtimes
├── swarm
├── tmp
│   └── moby-detect-rro1213774514
└── volumes
    ├── backingFsBlockDev
    └── metadata.db

376 directories, 203 files

~~~

## disk space 

sudo du -h --max-depth=1 /var/lib/docker | sort -hr

~~~
1.4G	/var/lib/docker/overlay2
1.4G	/var/lib/docker
2.3M	/var/lib/docker/image
104K	/var/lib/docker/buildkit
80K	/var/lib/docker/containers
56K	/var/lib/docker/network
28K	/var/lib/docker/volumes
8.0K	/var/lib/docker/tmp
8.0K	/var/lib/docker/plugins
4.0K	/var/lib/docker/swarm
4.0K	/var/lib/docker/runtimes




~~~