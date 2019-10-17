---
marp: true
theme: gaia
class: lead
---

# Not your Daddy's Docker 101

by John Goodwin

---

# Intro

- Metabolon, Inc
  - <https://www.metabolon.com/>
- Principal Software Engineer
- Writing software professionally since 1997

![Metabolon Logo](images/metabolon-logo.png)

---

## Agenda

- Attendee Intentions
- Motivation
- Docker in 60 seconds
- Demo
- Decomposition of Demo
- Bonus - Understanding Layers
- Q&A
- Resources

---

## Attendee Intentions

At this time, want to ask each person what they hoped this talk would cover.

---

## Motivation

- Why a talk like this?
- Short story first

---

## Sports Hobby - Endurance Races

![First race face](images/first-sprint-finish-last-anguish_larger.jpg)

---

![After Image](images/after-image-20170216_h800.jpg)

---

## Quick poll

- Is running a two legged exercise?
- Is moving your hands/arms wasted energy?

---

- Sprinter [Usain Bolt Slow Motion 2015 HD](https://www.youtube.com/watch?v=yhaxKsBzGfw)

---

## Docker in 60 seconds

- <https://docs.docker.com/engine/docker-overview/>

---

## Demo

```shell
docker run python:3.7-alpine python3 --version
docker run python:3.7-alpine python3 -c 'print("Hello codecamp!")'
```

---

## Process

```shell
docker ps -a
docker inspect
```

- Path
- Args
- State

---

## Environment

- Config

---

## Storage / Mounts

- Union Filesystems
- Mounts

---

## Network

- resolv.conf
- hostname
- hosts
- NetworkSettings

---

## cgroups

- what are cgroups
- HostConfig

---

> cgroups (abbreviated from control groups) is a Linux kernel feature that limits, accounts for, and isolates the resource usage (CPU, memory, disk I/O, network, etc.) of a collection of processes.
> Engineers at Google (primarily Paul Menage and Rohit Seth) started the work on this feature in 2006 under the name "process containers".
>> source <https://en.wikipedia.org/wiki/Cgroups>

---

## pipelining

```shell
docker run --rm python:3.7-alpine python3 --version > version.txt && cat version.txt
```

![Std Streams](images/Stdstreams-notitle.svg)

---

## signals

- <https://www.gnu.org/software/libc/manual/html_node/Termination-Signals.html>
- entrypoint vs command

```shell
docker run --rm -it --mount type=bind,source=$(pwd)/sigterm.py,dst=/tmp/sigterm.py python:3.7-alpine python3 /tmp/sigterm.py
```

---

(note this is the same)

```shell
docker run --rm -it --mount type=bind,source=$(pwd)/sigterm.py,dst=/tmp/sigterm.py --entrypoint=/bin/sh python:3.7-alpine -c "python3 /tmp/sigterm.py"
```

---

(but this hangs)

```shell
docker run --rm -it --mount type=bind,source=$(pwd),dst=/app python:3.7-alpine /app/callsigterm.sh
```

---

## Bonus - Understanding Layers

```shell
dive python:3.7-alpine
```

---

## Q&A

### Questions

---

## Resources

- <https://docs.docker.com/>
- <https://katacoda.com/>
- <https://github.com/wagoodman/dive>
- <https://github.com/marp-team/marp-vscode>
  - <https://github.com/marp-team/marp-cli/>
  - Used to transform markdown to slides
