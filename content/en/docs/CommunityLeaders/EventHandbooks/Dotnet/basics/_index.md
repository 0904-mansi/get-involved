---
title: "Basics of Docker"
linkTitle: "Basics of Docker"
weight: 806
description: >-
     Understanding Basics of Docker
---

- [Main Components of Docker System](#main-components-of-docker-system)
- [Test Your Knowledge](#test-your-knowledge)

##  Basics of Docker

This section introduces the basic terminology of Docker.

Docker is a platform for developers and sysadmins to build, ship, and run applications. Docker lets you quickly assemble applications from components and eliminates the friction that can come when shipping code. Docker lets you test and deploy your code into production as fast as possible.

Docker simplifies software delivery by making it easy to build and share images that contain your application’s entire environment, or _application operating system_.

## What does it mean by an application operating system ?

Your application typically requires a specific version of operating system, application server, runtime, and database server. It may also require configuration files, and multiple other dependencies. The application may need binding to specific ports and certain amount of memory. The components and configuration together required to run your application is what is referred to as application operating system.

You can certainly provide an installation script that will download and install these components. Docker simplifies this process by allowing to create an image that contains your application and infrastructure together, managed as one component. These images are then used to create Docker containers which run on the container virtualization platform, provided by Docker.

## Main Components of Docker System

Docker has three main components:

- Images are the *build component* of Docker and are the read-only templates defining an application operating system.
- Containers are the *run component* of Docker and created from images. Containers can be run, started, stopped, moved, and deleted.
- Images are stored, shared, and managed in a registry and are the *distribution component* of Docker. 
- DockerHub is a publicly available registry and is available at http://hub.docker.com.

In order for these three components to work together, the *Docker Daemon* (or Docker Engine) runs on a host machine and does the heavy lifting of building, running, and distributing Docker containers. In addition, the *Client* is a Docker binary which accepts commands from the user and communicates back and forth with the Engine.

![docker-architecture](docker-architecture.png)


The Client communicates with the Engine that is either co-located on the same host or on a different host. Client uses the `pull` command to request the Engine to pull an image from the registry. The Engine then downloads the image from Docker Store, or whichever registry is configured. Multiple images can be downloaded from the registry and installed on the Engine. Client uses the `run` run the container.

## Docker Image

We've already seen that Docker images are read-only templates from which Docker containers are launched. Each image consists of a series of layers. Docker makes use of union file systems to combine these layers into a single image. Union file systems allow files and directories of separate file systems, known as branches, to be transparently overlaid, forming a single coherent file system.

One of the reasons Docker is so lightweight is because of these layers. When you change a Docker image—for example, update an application to a new version— a new layer gets built. Thus, rather than replacing the whole image or entirely rebuilding, as you may do with a virtual machine, only that layer is added or updated. Now you don't need to distribute a whole new image, just the update, making distributing Docker images faster and simpler.

Every image starts from a base image, for example `ubuntu`, a base Ubuntu image, or `fedora`, a base Fedora image. You can also use images of your own as the basis for a new image, for example if you have a base Apache image you could use this as the base of all your web application images.

NOTE: By default, Docker obtains these base images from Docker Store.

Docker images are then built from these base images using a simple, descriptive set of steps we call instructions. Each instruction creates a new layer in our image. Instructions include actions like:

- Run a command
- Add a file or directory
- Create an environment variable
- Run a process when launching a container

These instructions are stored in a file called a Dockerfile. Docker reads this Dockerfile when you request a build of an image, executes the instructions, and returns a final image.

## Docker Container

A container consists of an operating system, user-added files, and meta-data. As we've seen, each container is built from an image. That image tells Docker what the container holds, what process to run when the container is launched, and a variety of other configuration data. The Docker image is read-only. When Docker runs a container from an image, it adds a read-write layer on top of the image (using a union file system as we saw earlier) in which your application can then run.

## Docker Engine

Docker Host is created as part of installing Docker on your machine. Once your Docker host has been created, it then allows you to manage images and containers. For example, the image can be downloaded and containers can be started, stopped and restarted.

### Docker Client

The client communicates with the Docker Host and let's you work with images and containers.

Check if your client is working using the following command:

```
docker -v
```

It shows the output:

```
Docker version 20.10.2, build 2291f61
```

NOTE: The exact version may differ based upon how recently the installation was performed.

The exact version of Client and Server can be seen using `docker version` command. This shows the output as:

```
 docker version
Client: Docker Engine - Community
 Cloud integration: 1.0.7
 Version:           20.10.2
 API version:       1.41
 Go version:        go1.13.15
 Git commit:        2291f61
 Built:             Mon Dec 28 16:12:42 2020
 OS/Arch:           darwin/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.2
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       8891c58
  Built:            Mon Dec 28 16:15:28 2020
  OS/Arch:          linux/amd64
  Experimental:     true
 containerd:
  Version:          1.4.3
  GitCommit:        269548fa27e0089a8b8278fc4fc781d7f65a939b
 runc:
  Version:          1.0.0-rc92
  GitCommit:        ff819c7e9184c13b7c2607fe6c30ae19403a7aff
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
ajeetraina@Ajeets-MacBook-Pro realtime-sensor-jetson % 
```

The complete set of commands can be seen using `docker --help`.


## Test Your Knowledge 


| S. No.   |    Question. |      Response
:--------| :--------------|:---------------|
| 1   | What is difference between Docker Image and Docker Container? | |
| 2   | Where are all Docker images stored? | |
| 3   | Is DockerHub a public or private Docker registry? | |
| 4   | What is the main role of Docker Engine? | |
