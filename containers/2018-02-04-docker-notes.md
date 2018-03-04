# Docker Notes
> :calendar: *February 19, 2018*

Notes from Katacoda's Docker course as well as the Docker docs.

### What Is Docker?

Docker allows you to run containers. A container is a sandboxed process running an application and
its dependencies on the host operating system. The application inside the container considers itself
to be the only process running on the machine while the machine can run multiple containers
independently.

### Installing Docker

Docker can be run on Windows, Mac, and Linux; however, non-Linux OSes require a hypervisor (HyperKit
on Mac, Hyper-V on Windows).

On all operating systems, you can also install Kitematic as a desktop GUI for Docker.

### Persisting Data

Most Docker applications will be stateless - meaning they can be killed and started without needing
any persisted data.

Sometimes you may need to persist data to the host machine. For example, you may be running a
database inside a container, or saving server logs to a file.

Passing the `-v` or `--volume` flag to `docker run` will bind a host directory to a directory in
the container.

Starting with Docker 17.06, you can now use the `--mount` flag to attach a filesystem mount to the
container. This is now the preferred way to persist data.

When an image defined a `VOLUME` in the Dockerfile, Docker will create an anonymous volume unless
you explicitly create a named volume.

If you need to directly access a volume, it's recommended to interact with it using a container. For
example, if you need to pre-populate a volume before mounting it on its intended application, you
can mount it to a container running Ubuntu and access it from there.

```bash
docker volume create REDIS_DATA_DIR

docker run \
--name redis \
--mount type=volume,source=REDIS_DATA_DIR,target=/data \
--publish 6379:6379 \
--restart unless-stopped \
--detach \
redis:latest redis-server --appendonly yes
```

See <https://docs.docker.com/storage/volumes/>

### Container Networking

Some containers don't need to communicate with the outside world and only need to interact with each
other. An example would be a blog application connected to a database.

You could run the blog and database on the host network (localhost). If the blog exposed port 80 and
the database exposed port 3306 (MySQL), then both containers would be accessible on `localhost:80`
and `localhost:3306` respectively.

You could also use the default bridge network, and bind the IP of the containers to `127.0.0.1` with
their respective exposed ports.

Docker does have a `--link` flag which allows containers to communicate with one another without
knowing their assigned IP addresses, but this feature is deprecated, so you should stop using it.

The recommended approach is to create a _user-defined network_. This sounds complicated, but it
really consists of running `docker network create USER_DEFINED_NETWORK`. User-defined networks have
and embedded DNS to resolve container names to IP addresses.

In order for the DNS to work, containers must be passed the `--name` and `--network` flags at
creation time. In the actual code for the application running in the container, you can use the
container name instead of the actual IP address, for example, `mongodb://my_mongo_container:27017`.

### Running a Container in the Foreground

In most cases you'll run Docker applications in the background, but sometimes you may want to run
one in the foreground.

The `-it` flag allows you to do just that. `-it` is shorthand for `--interactive --tty`.

Running `docker run -it node` will run the Node.js image in a container and give you access to the
Node REPL.

Running `docker run -it ubuntu /bin/bash` will run the Ubuntu image in a container and then run the
`bash` command giving you access to a `bash` prompt.

If you don't need the container to survive after you exit, you can also pass the `--rm` flag.

## Docker Commands

### `docker search`

Searches the Docker Hub registry for an image.

### `docker run`

Starts a container running the specified image. If the image isn't available locally, Docker will
pull the image from Docker Hub. By default, the `latest` version is used, unless specified.

Flags:
  * `-d, --detach` - runs the container in the background
  * `-p, --publish` - publishes a container's port to the host
  * `-v, --volume` - binds a host directory to a directory in the container
  * `-e, --env` - sets environment variables
  * `--name` - assigns a name to the container (Docker will generate a random name if not specified)
  * `--mount` - attaches a filesystem mount to the container
  * `--network` - connects the container to a specific network
  * `--restart` - set the restart policy for the container
  * `--rm` - automatically remove the container when it exits
  * `-it` - runs the container in the foreground with an interactive TTY; shorthand for `--interactive --tty`

See <https://docs.docker.com/engine/reference/commandline/run/>

### `docker stop`

Stops one or more running containers. Docker will attempt to stop the process inside the container
using `SIGTERM`, followed by `SIGKILL` after a grace period.

Pass the `--time` flag to specify how long to wait before sending the kill signal.

### `docker start`

Starts one or more stopped containers.

### `docker restart`

Restarts one or more containers. Pass the `--time` flag to specify how long to wait before killing
the container.

### `docker ps`

Lists all running containers. An alias for `docker container ls`.

### `docker rm`

Removes one or more containers.

### `docker rmi`

Removes one or more images. Shorthand for `docker image rm`.

### `docker inspect`

Returns information on Docker objects in JSON format.

See <https://docs.docker.com/engine/reference/commandline/inspect/>

### `docker logs`

Prints the logs present at the time of execution. Pass the `--follow` flag to continue streaming
logs.

### `docker port`

Lists port mappings for the container.

## Docker Container Commands

### `docker container ls`

Lists all running containers. Pass the `--all` flag to include stopped containers.

### `docker container prune`

Removes all stopped containers.

## Docker Image Commands

## `docker image ls`

Lists images. Pass the `--all` flag to view intermediate images.

## Docker Volume Commands

### `docker volume ls`

Lists volumes.

### `docker volume create`

Creates a volume that containers can use to consume and store data.

### `docker volume rm`

Removes one or more volumes.

### `docker volume prune`

Removes all unused volumes.

## Docker Network Commands

### `docker network create`

Creates a user-defined network. Pass the `--driver` flag to specify the network driver to use.

### `docker network connect`

Connect a container to a network. Use `docker network disconnect` to remove a container from a network.

### `docker network ls`

Lists available networks.

### `docker network rm`

Removes a network.

### `docker network prune`

Removes all unused networks.
