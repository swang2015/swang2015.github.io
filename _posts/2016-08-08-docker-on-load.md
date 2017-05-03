---
layout: post
title:  "Docker on Load"
date:   2016-08-08 7:00:00 +0800
categories: programmer infrastructure
tags: feature docker
background: /images/bg_whale.jpg
---

> I used docker at work a couple days ago, so here to give a short overview on what is docker and how to use it.

## What is Docker?

Docker is a hot containerization platform which wraps all the dependencies in an execution system and is easy to pack and ship as you go. What makes Docker so popular? Comparing to virtual machines, Docker is more portable and efficient. In Docker, operating systems and kernels are abstracted and shared, applications and everything else (e.g. code, runtime, system tools, system libraries) run in isolated space.

<div class="post-img">
	<img src="/images/docker_what.png" width="50%">
</div>

Docker automates the process of delivering software applications in a repeatable way which allows effective distributed system to get more deployments in a cloud. Its lightweight nature makes it easy for developers to quickly create and run containered applications. In a *container* applications are isolated and run securely with complete dependancies. You can run many containers simultaneously on a host. Each container is created from a Docker *image*. Here are some concepts that you need to know.

## Usage

| Concept | Description |
| --- | --- |
| image | A read-only template containing a series of *layers* stacked on top of each other. |
| container | Running instance of an image. |
| registry | Centralized host to store/manage/provide docker images. [Docker Hub](https://hub.docker.com/) is very popular and is hosted by *docker.com*. |
| Dockerfile | A text document that is essential to assemble an image. A Dockerfile contains a series of commands which are usually identical to the ordered ones when executing for in corresponding OS. Some typical instructions are [listed below](#dockerfile). |

*Docker.com* provides very [detailed docs](https://docs.docker.com/) about:

- [installation](https://docs.docker.com/engine/installation/)
- [docker CLI](https://docs.docker.com/engine/reference/commandline/docker/)
- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

After successfully installed docker on your machine, run `docker` in terminal to list all its options and commands. There are around 40 commands.

<div class="post-img">
	<img src="/images/docker_usage.png" width="65%">
</div>

### Dockerfile

It's as simple as running `docker build` with a *Dockerfile* to get an image built from scratch. In Dockerfiles, the proper format is like `INSTRUCTION arguments`. Here it introduces the basic docker instructions.

| Instruction | Usage |
| --- | --- |
| `FROM` | To specify base image, must be the first instruction. |
| `ENV` | To declare environment variables that can be reused. |
| `ADD` and `COPY` | To add and copy new files and directories to the container. |
| `RUN` and `CMD` | To execute commands. The difference between `RUN` and `CMD` is that only one `CMD` instruction will be called as default for an executing container. You sometimes need to declare `ENTRYPOINT` in order to cooperate with `CMD`, see [Understand how CMD and ENTRYPOINT interact](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact). |
| others | `EXPOSE` to listen on the network ports, <br> `VOLUME` to create and mount external volumes, <br> `WORKDIR` sets work directory. |

Dockerfile is a starting point to begin using docker (the other is just to pull images from public registry). Several examples of Dockerfile syntax are mentioned in [docker docs](https://docs.docker.com/engine/reference/builder/#dockerfile-examples) as well. Now you need to arm with knowledge of some docker commands.

### Playing with Docker

##### Manipulating images

- `docker build -t MYIMG .` to build image from Dockerfile -- don't forget the dot at the end of command line.
- `docker tag MYIMG NAME[:TAG]` to add tags to image.
- `docker rmi IMG1 IMG2 ...` to remove images.

##### Container lifecycle

- `docker run IMG` to create and start a container from an image. E.g. `docker run -it --name=SOMENAME IMG`
	- Options: `-i` for interactive session, `-t` for terminal interface, `-p` for exposing port, `-v` for mounting volumes.
- `docker start/stop/restart CONTAINER` to start/stop/stop and start a container.
- `docker attach CONTAINER` to connect to a running container, `CTRL-q` to detach.
- `docker exec CONTAINER COMMAND` to run a command in a container.
- `docker rm CONTAINER CONTAINER ...` to remove.

##### Info

- `docker images` shows all images in the engine.
- `docker ps` shows running containers, `docker ps -a` show running and complete ones.
- `docker logs CONTAINER` gets logs from container.


##### Registry

- `docker search NAME` to get pre-built image from registry.
- `docker pull REPOSITORY[:TAG]` to pull image/repository from registry, or just pull with filename if from Docker Hub.
- `docker push REPOSITORY[:TAG]` to push local image to registry.
- `docker commit CONTAINER [NAME[:TAG]]` to save container's change into a new image.


**Extensive reading:** [More tips](https://github.com/wsargent/docker-cheat-sheet#best-practices) about docker's best practices, security issues and other useful commands.
