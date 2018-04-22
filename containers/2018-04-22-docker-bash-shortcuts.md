# Docker Bash Shortcuts
> :calendar: _April 22, 2018_

Bash shortcuts for Docker commands with lots of arguments.

Save these in `/usr/local/bin` and `chmod +x` them.

### `docker-run.sh`

Shortcut for running a container in interactive mode and removing it once you exit the shell.

```bash
#!/bin/bash

set -e

DOCKER_ARGS=(
--interactive \
--tty \
--rm
)

set -- docker run "${DOCKER_ARGS[@]}" "$@"

exec "$@"
```

### `docker-exec.sh`

Shortcut for executing a command inside a container with an interactive shell.

Fixes the issue with column-width and line-height. See <https://github.com/moby/moby/issues/33794>.

```bash
#!/bin/bash

set -e

DOCKER_ARGS=(
--env COLUMNS="`tput cols`" \
--env LINES="`tput lines`" \
--interactive \
--tty
)

set -- docker exec "${DOCKER_ARGS[@]}" "$@"

exec "$@"
```
