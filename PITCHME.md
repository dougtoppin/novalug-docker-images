## Building Your Own Docker Images
##### <span style="font-family:Helvetica Neue; font-weight:bold"><span style="color:#e49436">NovaLUG, 13-May-2017</span>
<span style="color:#e49436">dougtoppin@gmail.com</span>

View this using [GitPitch](https://gitpitch.com/dougtoppin/novalug-docker-images)
---

## Agenda

* Overview
* What is Docker?
* Commands you need to use
* What are Docker images?
* Where can I find and store images?
* Links

---

## Overview

This is a continuation of my previous NovaLUG presentation on
[Docker For Everyone](https://github.com/dougtoppin/presentations/blob/master/novalug-dockerforeveryone.pdf)

Docker can be used to create customized images that match your needs or to distribute your application to others

If Docker is installed on your machine you can try this in real time

I am running Version 17.05.0-ce-mac9

+++

Install ready-to-go from here

[https://store.docker.com/search?type=edition&offering=community](https://store.docker.com/search?type=edition&offering=community)

+++

To build your own docker try this from the Moby project [https://mobyproject.org/](https://mobyproject.org/) (evolving, YMMV)

[https://github.com/moby/moby](https://github.com/moby/moby)


---
## What is Docker?

+++

Docker is tbd

"sandbox applications on a secure Linux environment"

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

## Commands you need to use


+++

Tell me something

* docker help - more than 50 subcommands
* docker version - who am i
* docker info - describe my environment

+++

Run stuff

* docker run - run something
* docker ps - what is running or has run
* docker exec - jump into something already running

+++

Images

* docker images - what is in my image cache
* docker build - make me something
* docker push - save my image somewhere

+++

Looking around a little

* docker logs - output from something running or that ran
* docker inspect - look at something

+++

Maintenance

* docker rm - remove containers
* docker rmi - remove images
* docker prune - clean up on a grander scale



---


## What are Docker images?

+++

let's talk about images

"binary blobs"


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

+++

Creating images

There are several ways to create images

* build using a Dockerfile
* commit a running container

+++

### tags

* versions
* latest
* customized

+++


Build an image with a tag using a Dockerfile

`docker build -t myalpine:latest .`

Using a tag helps because you can use that name to refer to it later

+++
Running images

Run using a tag

`docker run -it --rm myalpine`
+++

Commit a container (customized to your needs) to an image

```
docker run -it --rm --name=test1 alpine sh
docker container commit test1 dougtoppin/test1
```

+++


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

* registries - metadata (labels/tags/info) and pointers to repositories
* repositories - physical storage


+++
### store.docker.com (aka dockerhub)

+++

### RH container catalog

+++

### AWS ECR
+++

### DTR


+++
### files using export and import using archives

* docker image save
* docker image import
* docker container commit

+++
push an image somewhere

+++
image layers and vulnerabilities

image scanning

+++
image security

+++
content trust

---
## links

* [Docker For Everyone](https://github.com/dougtoppin/presentations/blob/master/novalug-dockerforeveryone.pdf)
* [https://www.docker.com/](https://www.docker.com/)
* [https://hub.docker.com/](https://hub.docker.com/)
* [https://github.com/moby/moby](https://github.com/moby/moby)
