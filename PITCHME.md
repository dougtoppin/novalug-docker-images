## Building Your Own Docker Images
##### <span style="font-family:Helvetica Neue; font-weight:bold"><span style="color:#e49436">NovaLUG, 13-May-2017</span>
<span style="color:#e49436">dougtoppin@gmail.com</span>

View this using [GitPitch](https://gitpitch.com/dougtoppin/novalug-docker-images)
---

## Agenda

* Overview
* What is Docker?
* What are Docker images?

---

## Overview

This is a continuation of my previous NovaLUG presentation on
[Docker For Everyone](https://github.com/dougtoppin/presentations/blob/master/novalug-dockerforeveryone.pdf)

Docker can be used to create customized images that match your needs or distribute your code to other users.

If Docker is installed on your machine you can try this in real time.

---
## What is Docker?

+++

Docker is tbd

+++

a little more tbd

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
## links

* [Docker For Everyone](https://github.com/dougtoppin/presentations/blob/master/novalug-dockerforeveryone.pdf)
* [https://www.docker.com/](https://www.docker.com/)
* [https://hub.docker.com/](https://hub.docker.com/)
