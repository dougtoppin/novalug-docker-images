## Building Your Own Docker Images
##### <span style="font-family:Helvetica Neue; font-weight:bold"><span style="color:#e49436">NovaLUG, 13-May-2017</span>
<span style="color:#e49436">dougtoppin@gmail.com</span>

View this using [GitPitch](https://gitpitch.com/dougtoppin/novalug-docker-images)
---

## Agenda

* Overview
* What is Docker?
* What are Docker images?
* Where can I find and store images?

---

## Overview

This is a continuation of my previous NovaLUG presentation on
[Docker For Everyone](https://github.com/dougtoppin/presentations/blob/master/novalug-dockerforeveryone.pdf)

Docker can be used to create customized images that match your needs or to distribute your application to others

If Docker is installed on your machine you can try this in real time

Install ready-to-go docker cli and engine from here

[https://store.docker.com/search?type=edition&offering=community](https://store.docker.com/search?type=edition&offering=community)

To build your own docker cli try [https://github.com/moby/moby](https://github.com/moby/moby)


I am running Version 17.05.0-ce-mac9

---
## What is Docker?

+++

Docker is tbd

+++

a little more tbd

---
The bigger picture

* microservices
* clusters (swarm, OpenShift, Kubernetes)
* cloud (Red Hat OpenShift, AWS ECS, MS Azure, Google GCP)
* logging and log aggregation
* security (engine, container, repository, image)

---

Commands you need to use

* docker help - more than 50 subcommands
* docker version - who am i?
* docker info - describe my environment
* docker ps - what is running or has run
* docker images - what is in my image cache
* docker build - make me something
* docker run - run something
* docker logs - output from something running/that ran
* docker inspect - look at something
* docker exec - jump into something already running
* docker push - save my image somewhere
* docker prune - clean up stuff



---


## What are Docker images?

+++

let's talk about images

+++

let's talk a little more about images

---

Dockerfiles

+++

example of a Dockerfile

```
FROM alpine
RUN something

```

+++ Creating images

Build using a tag

`docker build -t myalpine:latest .`

+++ Running images

Run using a tag

`docker run -it --rm myalpine`
---

## Dockerize an application

+++
existing code

```
something goes here
something else goes here
```

+++
dockerize it like this

---
## Where can I find and store images?

+++
store.docker.com (aka dockerhub)

+++
my own repository


---
## links

* [Docker For Everyone](https://github.com/dougtoppin/presentations/blob/master/novalug-dockerforeveryone.pdf)
* [https://www.docker.com/](https://www.docker.com/)
* [https://hub.docker.com/](https://hub.docker.com/)
* [https://github.com/moby/moby](https://github.com/moby/moby)
