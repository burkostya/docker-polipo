# Contents
- [Introduction](#introduction)
    - [Version](#version)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
    - [Data Store](#data-store)
- [Upgrading](#upgrading)

# Introduction
Dockerfile to build image with polipo proxy server.

## Version
Current Version: 1.1.1

# Installation

Pull specific version of the image from the docker index.

```bash
docker pull burkostya/polipo:1.1.1
```

Alternately you can build the image yourself.

```bash
git clone https://github.com/burkostya/polipo.git
cd polipo
docker build -t '<user>/polipo' .
```

# Quick Start
Run container

```bash
docker run --name='polipo' -it --rm \
  -p 3111:3111 \
  burkostya/polipo:1.1.1
```

Polipo web interface now available on `http://localhost:3111/polipo/`

# Configuration

## Cache Store
For cache persistency you should mount a volume

```bash
/var/cache/polipo
```

```bash
mkdir /opt/data/polipo/cache
docker run --name='polipo' -d \
  -p 3111:3111 \
  -v /opt/data/polipo:/var/cache/polipo \
  burkostya/polipo:1.1.1
```

# Upgrading

To upgrade to newer version of polipo, follow this steps:

- Update the docker image.

```bash
docker pull burkostya/polipo:1.1.1
```

- Stop the currently running image

```bash
docker stop polipo
docker rm polipo
```

- Optionaly. Backup the application cache by coping content of mounted volume

```bash
cp -r /opt/data/polipo/cache /some/poilpo/cache/backup/dir/
```

- Start the image

```bash
docker run -d --name polipo \
  -p 3111:3111\
  -v /opt/data/polipo/cache:/var/cache/polipo \
  burkostya/polipo:1.1.1
```
