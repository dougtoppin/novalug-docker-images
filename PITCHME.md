## Building Your Own docker Images
##### <span style="font-family:Helvetica Neue; font-weight:bold"><span style="color:#e49436">NovaLUG, 13-May-2017</span>
<span style="color:#e49436">dougtoppin@gmail.com</span>

---

## Agenda

* Overview
* What is docker?
* Commands you need to use
* What are docker images?
* Where can I find and store images?
* Links

---

## Overview

This is a continuation of my previous NovaLUG presentation on
[docker For Everyone](https://github.com/dougtoppin/presentations/blob/master/novalug-dockerforeveryone.pdf)

docker can be used to create customized images that match your needs or to distribute your application to others

If docker is installed on your machine you can try this in real time

I am running Version 17.05.0-ce-mac9

+++
### Where do I get docker?

+++

Install ready-to-go from here

[https://store.docker.com/search?type=edition&offering=community](https://store.docker.com/search?type=edition&offering=community)

+++

To build your own docker try this from the Moby project [https://mobyproject.org/](https://mobyproject.org/) (evolving, YMMV)

[https://github.com/moby/moby](https://github.com/moby/moby)


---
## What is docker?

+++

"Operating-system-level virtualization is a computer virtualization method in which the kernel of an operating system allows the existence of multiple isolated user-space instances, instead of just one. Such instances, which are sometimes called containers,[1] virtualization engines (VEs) or jails (FreeBSD jail or chroot jail), may look like real computers from the point of view of programs running in them."

"sandbox applications on a secure Linux environment"

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
* docker version - what am i running and talking to
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


## What are docker images?

+++

let's talk about images

"binary blobs"

"An image is an inert, immutable, file that's essentially a snapshot of a container. Images are created with the build command, and they'll produce a container when started with run. Images are stored in a Docker registry such as registry.hub.docker.com. Because they can become quite large, images are designed to be composed of layers of other images, allowing a miminal amount of data to be sent when transferring images over the network."

---

Dockerfiles

"A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.
Using docker build users can create an automated build that executes several command-line instructions in succession."

<a href="https://docs.docker.com/engine/reference/builder/" target="_blank">Dockerfile reference</a>

<a href="https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/" target="_blank">Dockerfile best practices</a>
+++

Key commands in them
* FROM - start with this (might be `scratch`)
* RUN - run this in a new layer on top of current layer
* COPY - copy from host filesystem into image filesystem
* ADD - more functional copy from host filesystem into image filesystem
* WORKDIR
+++
Key commands (cont)
 
* ENTRYPOINT - run this command in the image when the container starts
* CMD - default arguments for ENTRYPOINT
* ENV - set environment variables
* EXPOSE - this image needs these ports
* LABEL - add metadata to the image being built
+++

example of a Dockerfile

```
FROM alpine
LABEL maintainer "dougtoppin@gmail.com"
LABEL org.label-schema.vcs-url="https://github.com/dougtoppin/lenticular"
LABEL org.label-schema.description="Tool for creating lenticular images by combining two images"

COPY ./lenticulate.pl /tmp

WORKDIR /tmp

RUN [ "apk", "update" ]
RUN [ "apk", "add", "perl" ]
RUN [ "apk", "add", "perl-gd" ]

ENTRYPOINT [ "/tmp/lenticulate.pl" ]

```
+++
Review of how existing images were made

Click through to their Dockerfiles to see the details

* <a href="https://store.docker.com/images/postgres?tab=description" target="_blank">postgres</a>
* <a href="https://store.docker.com/images/centos?tab=description" target="_blank">centos</a>
* <a href="https://store.docker.com/images/perl?tab=description" target="_blank">perl</a>
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

---

## dockerize an application

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

### dockerhub

store.docker.com

+++

### Red Hat container catalog

"The <a href="https://access.redhat.com/containers" target="_blank">Red Hat container catalog</a> acts as a single location for finding, acquiring, and learning about all official Red Hat containers.
In time, this will expand to containers from Red Hat certified Independent Software Vendors (ISVs) as well."

+++

### AWS ECR
<a href="https://aws.amazon.com/ecr/" target="_blank">Amazon EC2 Container Registry (ECR) </a> is a fully-managed Docker container registry...hosts your images in a highly available and scalable architecture, allowing you to reliably deploy containers for your applications.

+++

### DTR

<a href="https://docs.docker.com/datacenter/dtr/2.1/guides/" target="_blank">Docker Trusted Registry (DTR) </a>  "is the enterprise-grade image storage solution from Docker. You install it behind your firewall so that you can securely store and manage the Docker images you use in your applications."

+++
### files using export and import using archives

Instead of using a registry you can work at the file level if so desired.

* docker image save
* docker image import
* docker container commit

+++
Store an image into a registry

Once you have authenticated with a respository you can store an image into it using the `docker push ...` command.

* docker login registry_url
* docker tag repository:image:version
* docker push repository:image:version
+++
image layers, vulnerabilities and scanning

Because images are composed of layers containing executable files those files may contain vulnerabilities due to either bugs or malicious code.
It is important to ensure that the images and layers comprising them in your repositories do not contain vulnerabilities.
Image scanning services exist to check image content and compare with known vulnerability databases.
Once detected you can determine what images in the repository and potentially deployed must be replaced with updated versions.

+++
image security and content trust

Images are cryptographically signed with another server such as <a href="https://github.com/docker/notary" target="_blank">Notary</a>.
This server is then communicated with when pulling the image to confirm that the image content has not changed and is still trusted based on key sets (organization, repository and temporal).

---
## links

* <a href="https://github.com/dougtoppin/presentations/blob/master/novalug-dockerforeveryone.pdf" target="_blank">Docker For Everyone</a>
* <a href="https://www.docker.com/" target="_blank">https://www.docker.com/</a>
* <a href="https://hub.docker.com/" target="_blank">https://hub.docker.com/</a>
* <a href="https://github.com/moby/moby" target="_blank">https://github.com/moby/moby</a>
