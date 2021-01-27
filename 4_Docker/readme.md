# Docker :whale: 

*`Dockerfile` builds `Image` runs `Container` - :artificial_satellite:*

- [Dockerfiles](#Dockerfiles)
- [Images](#Images)
- [Containers](#Containers)

## Dockerfiles

- to build the image run (don't forget the . and username & imagename are written small):

   `docker build -t USERNAME/IMAGENAME:TAGNAME .`  

- dockerfiles are build in read-only layers
- ephemeral: stopped, destroyed and reproducible with minimum effort
- current working directory of docker build is called `build context`
- only the last `CMD` in the dockerfile is executed
- `ADD` and `COPY` are similar, but `COPY` is preferred

- additional information to the often used `apt-get update`:
  - always combine `RUN apt-get update` with `apt-get install -y` in the same `RUN` statement (cache busting)
  - use version pinning where needed, e.g. `s3cmd=2.0.*`, check availability of [choosen version](https://packages.ubuntu.com/search?suite=default&section=all&arch=any&keywords=s3cmd&searchon=names)
  - avoid `RUN apt-get upgrade` or `dist-upgrade`
  - clean up the cache by removing `/var/lib/apt/lists`

```dockerfile
# Example of a dockerfile with the most common layers
FROM ubuntu:18.04
RUN apt-get update && apt-get install -y \
	curl \
	s3cmd=2.0.* \
	&& rm -rf /var/lib/apt/lists/*
COPY requirements.txt /tmp/
ENTRYPOINT ["echo", "Hello"]
CMD ["Peter"]
EXPOSE 80/tcp
ENV ADMIN_USER="Manny"
LABEL producer="Manthano"
USER user
```

- most common layers:
   - `FROM` creates a layer from an existing docker image | [From-reference](https://docs.docker.com/engine/reference/builder/#from)
     - `FROM [--platform=PLATFORM] IMAGENAME` or `FROM [--platform=PLATFORM] IMAGENAME:IMAGETAG`

   - `COPY` adds files from your Docker client’s current directory | [Copy-reference](https://docs.docker.com/engine/reference/builder/#copy)
     - `COPY [--chown=<user>:<group>] SOURCE DESTINATION`

   - `RUN` runs something in the shell | [Run-reference](https://docs.docker.com/engine/reference/builder/#run)
     - `RUN ["executable", "param1", "param2"]`

   - `CMD` provide defaults for an executing container, can be overwritten | [CMD-reference](https://docs.docker.com/engine/reference/builder/#cmd)
     - `CMD ["executable", "param1", "param2"]` or
     - `CMD ["param1", "param2"]` (if combined with ENTRYPOINT)

   - `LABEL` add one ore more labels | [Label-reference](https://docs.docker.com/engine/reference/builder/#label)
     - `LABEL KEY=VALUE KEY=VALUE`

   - `EXPOSE` expose a specific port | (use traditional ports of applications) [Expose-reference](https://docs.docker.com/engine/reference/builder/#expose)
     - `EXPOSE PORT`

   - `ENV` create environment variables | [Env-reference](https://docs.docker.com/engine/reference/builder/#env)
     - `ENV KEY=VALUE`

   - `ENTRYPOINT` configure a container that will run as an executable | [Entrypoint-reference](https://docs.docker.com/engine/reference/builder/#entrypoint)
     - `ENTRYPOINT ["executable", "param1", param2"]`, entrypoint executables and params are fixed, only following `CMD` can be overwritten
     - `CMD ["param1", param2"]`, those parameters are defaultly executed after the entrypoint, but can be overwritten

   - `USER` set the user for the image
     - `USER USER[:GROUP]` or `UID[:GID]`
     
   - [Other layers](https://docs.docker.com/engine/reference/builder) which are not discussed: `WORKDIR` `ARG` `ONBUILD` `STOPSIGNAL` `HEALTHCHECK` `SHELL`

## Docker-Commands

### Images

- see a list of all images:

   `docker images`

- run specific image:

   `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`

- delete a specific image:

  - remove by id: `docker rmi IMAGEID`

  - remove by name:`docker rm USERNAME/IMAGENAME:TAGNAME`

### Containers

- run a stopped container:

   `docker start`

- see a list of all containers:

   `docker ps -a`