# Docker compose

is useful:

- when you need to start multiple containers which work together
  - it automatically creates shared network
  - parameters are saved in a file instead of multiple positional arguments on multiple docker run commands
- when your software runs on a single host and you do not want to bother with kubernetes 

## install

[Offcial](https://docs.docker.com/compose/install/)

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

## usage cli

```
# start container in backround
docker-compose up -d 

# remove containers, network and (unnamed) volumes
docker-compose down 

# remove containers, networks and volumes
docker-compose down -v

# show logs of services
docker-compose logs -f

# if a new image for a service is avaiable update it
docker-compose up -d --force-recreate

# or with
docker-compose pull
docker-compose restart


```

## usage docker-compose.yml

[Docker compose file reference](https://docs.docker.com/compose/compose-file/)

- `image` reference a docker image for the service
- `build` build a docker image for the service (usage instead of image) 
- `command` Override the default command of the docker image of the service
- `container_name` set a specific container name (without one would be generated `<imageName>-<serviceName>`)
- `restart` defaults to `no`. Other options are: always, on-failure, unless-stopped
- `environment:` to define a list of environment variables. Boolean values need to be quoted so the yaml parser does not interfere
- `volumes` can be defined on service level or shared for every container on root level of the yaml [see](https://docs.docker.com/compose/compose-file/#volumes).There is a long form where you can configure more things and a short form which works similar to the usual -v flag in docker run: `[SOURCE:]TARGET[:MODE]`.

## noteworthy
By default Docker compose searches for a ./docker-compose.yml file 
- By default Compose sets up a single network for your app, so that the containers can communicate with each other by their container name.
- Valid top-level sections for a Compose file are: version, services, networks, volumes, and extensions starting with "x-"
