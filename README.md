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
as my [jrb93/alpinetini](https://github.com/jrb93/alpinetini-base) image or even to a FROM scratch image.

#### Multi-Stage Dockerfile ####

For example to build this [Mandelbrot](https://github.com/marijnfs/gomandel) generator
using "go get" simply create a new Dockerfile containing. ***Note** if you want to make a **FROM scratch**
image make sure **CGO_ENABLED=0** is set as an environment variable:

```Dockerfile
FROM jrb93/golangtini:1.9 as builder
ENV CGO_ENABLED=0
RUN go get -v github.com/marijnfs/gomandel

FROM scratch
COPY --from=builder /go/bin/gomandel .
ENTRYPOINT [ "./gomandel" ]
```

Build it:

```ShellSession
docker build -t gomandel .
```

Run it:

```ShellSession
docker run -v ${PWD}:/data gomandel --aa 4 -xres 1920 -yres 1080 -out /data/mandel.png
```

This will generate a png image and with the '-v' option it will mount the current directory
where the command was run from into the container, allowing you to view the image on the host
pc.