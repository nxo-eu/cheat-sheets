```yaml
title: Docker CLI
category: Devops
layout: 2022/sheet
```

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [Docker](#Docker)
	* 1.1. [`docker build`](#dockerbuild)
	* 1.2. [`docker run`](#dockerrun)
		* 1.2.1. [Example](#Example)
	* 1.3. [`docker create`](#dockercreate)
		* 1.3.1. [Example](#Example-1)
	* 1.4. [`docker exec`](#dockerexec)
		* 1.4.1. [Example](#Example-1)
	* 1.5. [`docker start`](#dockerstart)
	* 1.6. [`docker ps`](#dockerps)
	* 1.7. [`docker logs`](#dockerlogs)
	* 1.8. [`docker images`](#dockerimages)
	* 1.9. [`docker rmi`](#dockerrmi)
* 2. [Clean up](#Cleanup)
	* 2.1. [Clean all](#Cleanall)
	* 2.2. [Containers](#Containers)
	* 2.3. [Images](#Images)
	* 2.4. [Volumes](#Volumes)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

##  1. <a name='Docker'></a>Docker

Manage images
-------------

###  1.1. <a name='dockerbuild'></a>`docker build`

```sh
$ docker build [options] .
	  -t "app/container_name"    # name
	  --build-arg APP_HOME=$APP_HOME    # Set build-time variables
```

Create an `image` from a Dockerfile.


###  1.2. <a name='dockerrun'></a>`docker run`

```sh
$ docker run [options] IMAGE
	  # see `docker create` for options
```

####  1.2.1. <a name='Example'></a>Example

```sh
$ docker run -it debian:buster /bin/bash
```
Run a command in an `image`.

Manage containers
-----------------

###  1.3. <a name='dockercreate'></a>`docker create`

```sh
$ docker create [options] IMAGE
	  -a, --attach               # attach stdout/err
	  -i, --interactive          # attach stdin (interactive)
	  -t, --tty                  # pseudo-tty
	      --name NAME            # name your image
	  -p, --publish 5000:5000    # port map (host:container)
	      --expose 5432          # expose a port to linked containers
	  -P, --publish-all          # publish all ports
	      --link container:alias # linking
	  -v, --volume `pwd`:/app    # mount (absolute paths needed)
	  -e, --env NAME=hello       # env vars
```

####  1.3.1. <a name='Example-1'></a>Example

```sh
$ docker create --name app_redis_1 \
  --expose 6379 \
  redis:3.0.2
```

Create a `container` from an `image`.

###  1.4. <a name='dockerexec'></a>`docker exec`

```sh
$ docker exec [options] CONTAINER COMMAND
	  -d, --detach        # run in background
	  -i, --interactive   # stdin
	  -t, --tty           # interactive
```

####  1.4.1. <a name='Example-1'></a>Example

```sh
$ docker exec app_web_1 tail logs/development.log
$ docker exec -t -i app_web_1 rails c
```

Run commands in a `container`.


###  1.5. <a name='dockerstart'></a>`docker start`

```sh
$ docker start [options] CONTAINER
  -a, --attach        # attach stdout/err
  -i, --interactive   # attach stdin

$ docker stop [options] CONTAINER
```

Start/stop a `container`.


###  1.6. <a name='dockerps'></a>`docker ps`

```sh
$ docker ps
$ docker ps -a
$ docker kill $ID
```

Manage `container`s using ps/kill.


###  1.7. <a name='dockerlogs'></a>`docker logs`

```sh
$ docker logs $ID
$ docker logs $ID 2>&1 | less
$ docker logs -f $ID # Follow log output
```

See what's being logged in an `container`.


Images
------

###  1.8. <a name='dockerimages'></a>`docker images`

```sh
$ docker images
  REPOSITORY   TAG        ID
  ubuntu       12.10      b750fe78269d
  me/myapp     latest     7b2431a8d968
```

```sh
$ docker images -a   # also show intermediate
```

Manages `image`s.

###  1.9. <a name='dockerrmi'></a>`docker rmi`

```sh
$ docker rmi b750fe78269d
```

Deletes `image`s.

##  2. <a name='Cleanup'></a>Clean up

###  2.1. <a name='Cleanall'></a>Clean all

```sh
$ docker system prune
```

Cleans up dangling images, containers, volumes, and networks (ie, not associated with a container)

```sh
$ docker system prune -a
```

Additionally remove any stopped containers and all unused images (not just dangling images)

###  2.2. <a name='Containers'></a>Containers

```sh
# Stop all running containers
$ docker stop $(docker ps -a -q)

# Delete stopped containers
$ docker container prune
```

###  2.3. <a name='Images'></a>Images

```sh
$ docker image prune [-a]
```

Delete all the images

###  2.4. <a name='Volumes'></a>Volumes

```sh
$ docker volume prune
```

Delete all the volumes

Also see
--------

 * [Getting Started](http://www.docker.io/gettingstarted/) _(docker.io)_