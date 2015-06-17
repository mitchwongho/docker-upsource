# docker-upsource
Docker image of JetBrains' UpSource

## Usage

todo

## Create and mount an Upsource Data Volume Container

It's best to persist your Upsource data in a named Data Volume Container for the following reasons:
- decoupled for the application image upgrades
- can be backed-up, restored or migrated

```
$ sudo docker create \
    -v /opt/Upsource/conf \
    -v /opt/Upsource/data \
    -v /opt/Upsource/logs \
    -v /opt/Upsource/backups \
    --name upsource-data busybox /bin/true
```

## Install/Setup

Before running Upsource, configure the listen port `e.g. 8090`and
domain `e.g. localhost:8090` to assign to the instance.

N.B. The port specified for `--listen-port` and `--base-url` must be the same.

```
$ sudo docker run \
    --rm \
    --volumes-from upsource-data \
    -u=root \
    --name upsource
    oreomitch/docker-upsource:latest bin/upsource.sh configure \
    --listen-port 8090 \
    --base-url http://localhost:8090
```

## Run

To run Upsource, in a `debug` manner:

```
$ sudo docker run \
    -u=root \
    --rm \
    -p [host-port]:[container-port] \
    --volumes-from upsource-data \
    --name upsource
    oreomitch/docker-upsource:latest bin/upsource.sh run
```
Alternatively, the container can be launched by:
```
$ sudo docker run \
    -d
    -u=root \
    --rm \
    -p [host-port]:[container-port] \
    --volumes-from upsource-data \
    --name upsource
    oreomitch/docker-upsource:latest bin/upsource.sh run
```
