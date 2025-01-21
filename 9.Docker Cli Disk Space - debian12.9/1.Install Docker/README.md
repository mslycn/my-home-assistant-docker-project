
## apt  install docker.io

docker system df
~~~
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          0         0         0B        0B
Containers      0         0         0B        0B
Local Volumes   0         0         0B        0B
Build Cache     0         0         0B        0B
~~~

## tree
cd /var/lib/containerd

/var/lib/containerd# sudo tree  ./ -L 5

sudo tree /var/lib/containerd -L 5

~~~
./
├── io.containerd.content.v1.content
│   └── ingest
├── io.containerd.metadata.v1.bolt
│   └── meta.db
├── io.containerd.runtime.v1.linux
├── io.containerd.runtime.v2.task
├── io.containerd.snapshotter.v1.blockfile
├── io.containerd.snapshotter.v1.btrfs
├── io.containerd.snapshotter.v1.native
│   └── snapshots
├── io.containerd.snapshotter.v1.overlayfs
│   └── snapshots
└── tmpmounts

~~~

## disk 

sudo du -h --max-depth=1 /var/lib/containerd | sort -hr
~~
du -h --max-depth=1 /var/lib/containerd | sort -hr
144K	/var/lib/containerd
80K	/var/lib/containerd/io.containerd.metadata.v1.bolt
24K	/var/lib/containerd/io.containerd.content.v1.content
8.0K	/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs
8.0K	/var/lib/containerd/io.containerd.snapshotter.v1.native
4.0K	/var/lib/containerd/tmpmounts
4.0K	/var/lib/containerd/io.containerd.snapshotter.v1.btrfs
4.0K	/var/lib/containerd/io.containerd.snapshotter.v1.blockfile
4.0K	/var/lib/containerd/io.containerd.runtime.v2.task
4.0K	/var/lib/containerd/io.containerd.runtime.v1.linux
~~


## tree



tree /var/lib/docker -L 5

~~~
./
├── buildkit
│   ├── cache.db
│   ├── containerdmeta.db
│   ├── content
│   │   └── ingest
│   ├── executor
│   ├── history.db
│   ├── metadata_v2.db
│   └── snapshots.db
├── containers
├── engine-id
├── image
│   └── overlay2
│       ├── distribution
│       ├── imagedb
│       │   ├── content
│       │   │   └── sha256
│       │   └── metadata
│       │       └── sha256
│       ├── layerdb
│       └── repositories.json
├── network
│   └── files
│       └── local-kv.db
├── overlay2
│   └── l
├── plugins
│   ├── storage
│   │   └── ingest
│   └── tmp
├── runtimes
├── swarm
├── tmp
└── volumes
    ├── backingFsBlockDev
    └── metadata.db

~~~

## disk space 

sudo du -h --max-depth=1 /var/lib/docker | sort -hr

~~~
/var/lib/docker# sudo du -h --max-depth=1 /var/lib/docker | sort -hr
260K	/var/lib/docker
104K	/var/lib/docker/buildkit
40K	/var/lib/docker/network
40K	/var/lib/docker/image
28K	/var/lib/docker/volumes
16K	/var/lib/docker/plugins
8.0K	/var/lib/docker/overlay2
4.0K	/var/lib/docker/tmp
4.0K	/var/lib/docker/swarm
4.0K	/var/lib/docker/runtimes
4.0K	/var/lib/docker/containers


~~~