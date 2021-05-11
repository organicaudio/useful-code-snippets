# Docker persisting data

Docker does not persist data when a container is shutdown. In order to do so you need to define volumes or bind mounts.

## volumes

[official documentation](https://docs.docker.com/storage/volumes/)


- preferred way to persist data
- Are managed on host under: /var/lib/docker/volumes/
- can be named or anonymous
- create a volume: `docker volume create <volumeName>`
- -v  or --volumes parameter consists of three fields, separated by colon characters (:).
    1.  first field is the name of the volume
    2.  path where the file or directory are mounted in the container.
    3.  optional comma-separated list of options

**pitfall: the folder in the container will be overridden with the one from the host if it exists. When the folder on the host does not exists it will be created and the content of the folder on the docker container will be copied to the host.**


```shell
# create a named volume
docker volume create myvolume

# use a named volume on hello-world image
docker run -v myvolume:/usr/share/importantPath hello-world

# create a anonymous volume on hello-world image
docker run -v /usr/share/importantPath hello-world
```

Difference between defining VOLUME in a Dockerfile and adding a volume when starting a container:

- VOLUME creates a anonymous volume even when docker run does not specify a -v parameter
- [stackoverflow](https://stackoverflow.com/questions/40163036/difference-between-volume-declaration-in-dockerfile-and-v-as-docker-run-paramet)
- [docker forum](https://forums.docker.com/t/whats-the-difference-between-adding-volume-in-a-dockerfile-and-running-an-image-with-volume/17480)