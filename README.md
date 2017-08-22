# docker-redis-cluster

[![Docker Stars](https://img.shields.io/docker/stars/grokzen/redis-cluster.svg)](hub])
[![Docker Pulls](https://img.shields.io/docker/pulls/grokzen/redis-cluster.svg)](hub])
[![Image Size](https://img.shields.io/imagelayers/image-size/grokzen/redis-cluster/latest.svg)](https://imagelayers.io/?images=grokzen/redis-cluster:latest)
[![Image Layers](https://img.shields.io/imagelayers/layers/grokzen/redis-cluster/latest.svg)](https://imagelayers.io/?images=grokzen/redis-cluster:latest)

Docker image with redis built and installed from source.

The main usage for this container is to test redis cluster code. For example in https://github.com/Grokzen/redis-py-cluster repo.

The cluster is 6 redis instances running with 3 master & 3 slaves, one slave for each master. They run on ports 7000 to 7005.

It also contains 2 standalone instances that is not part of the cluster. They are running on port 7006 & 7007

The image will build the tag `3.0.6` from the redis git repo.

This image requires `Docker` above version 1.0



# Available tags

The following tags with pre-built images is available on `docker-hub`. They are based on the tags in this repo.

- Latest  (Is the highest tag that currently exists in the redis repo [3.2-rc1 currently])
- 3.2-rc1  (See 3.2.x branch)
- 3.0.6  (Built from master branch)
- 0.2.1  (Based on one of the earlier 3.0.x redis tags. Should no longer be used)



# Usage

If you want to use `docker-compose (fig)` please read next section.

Either download the latest build from docker hub with `docker pull grokzen/redis-cluster:3.0.6` and run it with `docker run -i -t grokzen/redis-cluster:3.0.6`.

Or to build the image, use either `make build` or `make rebuild`. It will be built to the image name `grokzen/redis-cluster`.

To start the image use `make run`. It will be started in the background. To gain access to the running image you can get a bash session by running `make bash`.

Redis cli can be used with `make cli` to gain access to one of the cluster servers.



# Docker compose (fig)

This image contains a `compose.yml` file that can be used with `docker-compose (fig)` to run the image. Docker compose is simpler to use then the old `Makefile`.

Build the image with `docker-compose -f compose.yml build`.

Start the image after building with `docker-compose -f compose.yml up`. Add `-d` to run the server in background/detatched mode.



# Known Issues

If you get a error when rebuilding the image that docker can't do dns lookup on `archive.ubuntu.com` then you need to modify docker to use google IPv4 DNS lookups. Read the following link http://dannytsang.co.uk/docker-on-digitalocean-cannot-resolve-hostnames/ and uncomment the line in `/etc/default/docker` and restart your docker daemon and it should be fixed.
