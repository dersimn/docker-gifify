# gifify-docker

A docker container for [gifify](https://github.com/vvo/gifify). Based on the work of [maxogden](https://github.com/maxogden/gifify-docker) and [STRML](https://github.com/STRML/gifify-docker).

![docker-badge](http://dockeri.co/image/dersimn/gifify)

# Installation

1. install docker
2. run `docker run -it --rm -v $(pwd):/data dersimn/gifify source.mov -o output.gif`

When you run `docker run dersimn/gifify` it executes the `gifify` command in `/data` inside the docker ubuntu VM, so in order for this to work you must mount your current working directory as `/data` in the volume. This is what `-v $(pwd):/data` does in the command above.  
You could also specify this command as an alias in your `.bashrc` file, for e.g.:

    alias gifify='docker run -it --rm -v $(pwd):/data dersimn/gifify'

and use it like

    gifify source.mov -o output.gif


## Usage Examples

    docker run -it --rm -v "$(pwd)":/data dersimn/gifify source.mov -o output.gif

Fit video in a 350x350 rectangle and don't scale up if it's smaller:

    docker run -it --rm -v "$(pwd)":/data dersimn/gifify source.mov -o output.gif --resize w=350:h=350:force_original_aspect_ratio=decrease


# Build

## Docker build

    docker build -f Dockerfile-debian -t dersimn/gifify .
    docker build -f Dockerfile-alpine -t dersimn/gifify:alpine .

## buildx

## buildx

    docker buildx create --name mybuilder
    docker buildx use mybuilder

    docker buildx build \
        -f Dockerfile-debian \
        --platform linux/amd64,linux/arm64/v8 \
        -t dersimn/gifify \
        -t dersimn/gifify:debian \
        --push \
        .

    docker buildx build \
        -f Dockerfile-alpine \
        --platform linux/amd64,linux/arm64/v8 \
        -t dersimn/gifify:alpine \
        --push \
        .