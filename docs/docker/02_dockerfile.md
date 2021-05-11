# Dockerfile

[Docker file reference](https://docs.docker.com/engine/reference/builder/)
[Nice summary of run, cmd and entypoint](https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/)

## Create image form dockerfile

- `docker build <context>`  builds Docker images from a Dockerfile and a 'context'.
- context is the set of files located in the specified PATH or URL
- the context is processed recursively
- `docker build .` is used to build a image based on a dockerfile in the current directory.
- use `-t <tageName>` to add a tag to the image

Simplistic docker file for java application:

```dockerfile
FROM openjdk:8-jdk-alpine
COPY target/*.jar app.jar
ENTRYPOINT["java", "-jar", "app.jar"]
```

## shell form vs. exec form

- the forms can be distinguished by their syntax. 
- they differ in their behavior.
- some docker commands like RUN, ENTRYPOINT or CMD can be used in either form.

shell form: 

- syntax: `<instruction> <command>`
- like calling `/bin/sh -c <command>`
- variable substitution works e.g. `exec echo $path`
- application which is started this way will not receiving interrupt signals (like crlt + c)

exec form:

- syntax: `<instruction> ["executable", "arg1", "arg2", ...]`
- like calling: `executable` directly, so it must be a valid path (/bin/echo instead of echo)
- preferred for CMD and ENTRYPOINT
- no variable replacement ($PATH does not work)

## dockerfile commands

RUN, CMD and Entrypoint all execute a command, but:

- **RUN** creates a new layer on the union file system
- **CMD** sets default command to run when container starts. This command can be replaced by another command by calling: `docker run -it <image> <command which is used instead>`
- **ENTRYPOINT** sets default command to run when container starts, but cannot be overwritten (exec and shell form). You can add a CMD without a command/executable afterwards to add further arguments to the entrypoint command which can be overwritten (only in exec form).

--> Use RUN for new layer and prefer ENTRYPOINT over CMD if you do not need to change arguments.

COPY and ADD copy files to an image and create a new layer, but:

- **COPY** can only be used on local files
- **ADD** can download any URL and extract tar balls

--> use COPY for local files

- **ENV** sets a environment variable (`ENV path=/opt/`) at docker build and during runtime.
- **ARG** defines parameters of a docker image which can be overridden when the images is build (e.g. `$ docker build --build-arg arg_name=blubb .`). only available during build time.

## useful images

A list of relatively small images. If present alpine images tend to be the smallest. Docker repositories mostly are organized via the tags (:8-jdk-alpine, :11-jdk-buster etc.).

Java:

- [openjdk:8-jdk-alpine](https://hub.docker.com/_/openjdk/)
- [openjdk:11-jdk-buster](https://hub.docker.com/_/openjdk/)
- [openjdk:14-jdk-slim](https://hub.docker.com/_/openjdk/)
- [adoptopenjdk/openjdk8-openj9:alpine](https://hub.docker.com/r/adoptopenjdk/openjdk8-openj9)
- [adoptopenjdk/openjdk11:alpine](https://hub.docker.com/r/adoptopenjdk/openjdk11)

# dockerfile vs. command line

## -p vs EXPORT

EXPORT does not actually publish the given port. It is a documentation for the user. The user of a image needs to export the port via -p flag when running docker run.

## --volume vs. VOLUME

VOLUME creates a anonymous volume even when docker run does not specify a --volume parameter.