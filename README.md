# Golangtini #

`Golangtini` is a image for compiling [golang](https://golang.org) applications/software in a [Docker](https://www.docker.com) container.

## Overview ##

* Version **1.1.0**
* Combines [jrb93/alpinetini](https://github.com/jrb93/alpinetini-base) with the official [golang:alpine3.6](https://hub.docker.com/_/golang/) Dockerfile
* Go (golang) versions **1.9.2** & **1.8.5**

## Supported tags ##

* [![](https://images.microbadger.com/badges/version/jrb93/golangtini:1.9.svg)](https://microbadger.com/images/jrb93/golangtini:1.9 "Get your own version badge on microbadger.com"), [![](https://images.microbadger.com/badges/version/jrb93/golangtini.svg)](https://microbadger.com/images/jrb93/golangtini "Get your own version badge on microbadger.com") [(versions/1.9/Dockerfile)](https://github.com/jrb93/golangtini/tree/master/versions/1.9)
* [![](https://images.microbadger.com/badges/version/jrb93/golangtini:1.8.svg)](https://microbadger.com/images/jrb93/golangtini:1.8 "Get your own version badge on microbadger.com") [(versions/1.8/Dockerfile)](https://github.com/jrb93/golangtini/tree/master/versions/1.8)

### How to use ###

Starting from Docker 17.05 and up you can now do multi-stage builds as an alternative
to the builder pattern. Using a multi-stage Dockerfile with this image as it first stage,
you can compile you golang programs, and transfer the resulting binary to a new image such
as my [jrb93/alpinetini](https://github.com/jrb93/alpinetini-base) with the official [golang:alpine3.6](https://hub.docker.com/_/golang/) image or even to a FROM scratch image.
