# Docker networking

## access container from your hosts ip address

If you want to access a docker container by its host ip address you either add its ip address before the port mapping when starting the container or you use the host network type. If you want to use ipv6 you may need to set some further configurations.

```shell
# maps port 80 of the container to localhost:8080 of host
docker run -p 8080:80

# maps port 80 of the container to 192.168.178.123:8080 of host
docker run -p 192.168.178.123:8080:80
```

## network types

Copied from [network driver summary](https://docs.docker.com/network/):

- User-defined bridge networks are best when you need multiple containers to communicate on the same Docker host.
- Host networks are best when the network stack should not be isolated from the Docker host, but you want other aspects of the container to be isolated.
- Overlay networks are best when you need containers running on different Docker hosts to communicate, or when multiple applications work together using swarm services.
- Macvlan networks are best when you are migrating from a VM setup or need your containers to look like physical hosts on your network, each with a unique MAC address.
- Third-party network plugins allow you to integrate Docker with specialized network stacks.

## user-defined bridge

[official doc](https://docs.docker.com/network/bridge/)

A user-defined bridge allow that two containers in this network can access each other via their container name (dns resolution). Container without a explicit network are in the default network bridge. The default bridge have no dns server so the containers need to address each other via their ip address. You can get the ip address of a container via `docker inspect <containerName>`.

```shell
# create a new bridge network
docker network create --driver bridge <bridgeName>

# list networks
docker network ls

# start container a contgainer in the network 
docker run --network=<bridgeName> <imageName>

# add a running container to a network
docker network connect <bridgeName> <runningContainerName>
```