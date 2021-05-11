# Docker CLI useful command

- [vs code plugin for docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) is pretty nice.
- official overview of [docker cli commands](https://docs.docker.com/engine/reference/commandline/docker/).

- `docker build . -t crowdsalat/imageName:tag` creates a image based on a Dockerfile and the context/ working directory and subdirectories
- `docker run <image>` starts a container from an image
    - `-d` run as daemon
    - `-it` runs interactively so you can execute commands in container (-t Allocate a pseudo-tty, -i Keep STDIN open )
    - `docker run -it --entrypoint sh crowdsalat/imageName:tag` starts a container and starts a interactive shell.
    - `-p 500:1000` maps the port 1000 of the container to the port 500 of the host. Reachable under localhost on the host system.
    - `-p 192.168.178.123:1000:500` maps the port 1000 of the container to the port of the host. Reachable under localhost on the host system. Reachable under the IP address of the host system.
    - `-v /var/logs/` binds /var/logs inside the container to a unnamed volume on the mount which resides in /var/lib/docker/volumes/
    - `-v /var/run/docker.sock:/var/run/docker.sock` containers started inside of this container will be started on the host a not inside the container (sibling not a child). Useful in CI/CD pipelines which uses containers as runners see: https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/
    - `-e VAR1=bla -e VAR2=blubb` defines environmental variables in the container
    - `—rm` remove container after it is stopped.
    - `—name` add name to the container.
- `docker history --no-trunc <image>` show something similar to the original dockerfile
- `docker exec -it container_name bash` connects to a running container with the name container_name
- `docker ps −a` shows all running docker container on a client
- `docker image / container / network / volumes / system`
      - ls
      - rm
      - inspect
- `docker system prune` removes:
    1. all stopped containers (`docker container prune`)
    2. all networks not used by at least one container (`docker network prune`)
    3. all dangling images (`docker image prune`)
    4. all dangling build cache
- `docker network create --driver bridge <bridgeName>` create a new bridge network
- `docker volume create <volumeName>` create a new bridge volume
- `docker cp <containerName>:<pathInConainer> <pathOnHost>`  copies data from the container to the host. Helpful if volume were not set up correct 


**If you pull a image with the latest tag it will first try to download it from docker hub and only if it is not there it will use a local variant.**
