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

I personally prefer a native Linux environment, so I do everything either on a dedicated Dell Ubuntu
laptop, or a VMware Ubuntu Server virtual machine.

**Install Dependencies**

```bash
sudo apt-get update && sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
```

**Add Docker's GPG Key**

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

**Add Docker's APT Repository**

```bash
sudo touch /etc/apt/sources.list.d/docker.list

echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable edge" | sudo tee /etc/apt/sources.list.d/docker.list
```

**Install Docker**

```bash
sudo apt-get update && sudo apt-get install docker-ce
```

**Add User to `docker` Group**

```bash
sudo groupadd docker

sudo usermod -aG docker $USER
```

You should now be able to run Docker commands without `sudo`. 

The Docker daemon should be running at boot. If not, run `sudo systemctl enable docker`.

### Persisting Data

Most Docker applications will be stateless - meaning they can be killed and started without needing
any persisted data.

Sometimes you may need to persist data to the host machine. For example, you may be running a
database inside a container, or saving server logs to a file.

Passing the `-v` or `--volume` flag to `docker run` will bind a host directory to a directory in
the container.

Starting with Docker 17.06, you can now use the `--mount` flag to attach a filesystem mount to the
container. This is now the preferred way to persist data.

```bash
# note: docker will create the volume if it doesn't exist
docker volume create redis

docker run \
--detach \
--name redis \
--mount source=redis,target=/data \
--publish 6379:6379 \
redis:latest
```

See <https://docs.docker.com/storage/volumes/>

### Running a Container in the Foreground

In most cases you'll run Docker applications in the background, but sometimes you may want to run
one in the foreground.

The `-it` flag allows you to do just that.

Running `docker run -it node` will run the Node.js image in a container and give you access to the
Node REPL.

Running `docker run -it ubuntu /bin/bash` will run the Ubuntu image in a container and then run the
`bash` command giving you access to a `bash` prompt.

## Docker Commands

### `docker search`

Searches the Docker Hub registry for an image.

### `docker run`

Starts a container running the specified image. If the image isn't available locally, Docker will
pull the image from Docker Hub. By default, the `latest` version is used, unless specified.

Flags:
  * `-d, --detach` - runs the container in the background
  * `-p, --publish` - publishes a container's port to the host.
  * `-v, --volume` - binds a host directory to a directory in the container to persist data
  * `-e, --env` - sets environment variables
  * `--name` - assigns a name to the container (Docker will generate a random name if not specified)
  * `--mount` - attaches a filesystem mount to the container
  * `--network` - connects the container to a specific network
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

Lists all running containers. An alias for `docker container list`.

### `docker rm`

Removes one or more containers.

### `docker rmi`

Removes one or more images.

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
