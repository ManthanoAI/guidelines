# Docker :whale: 

"`Dockerfile` builds `Image` runs `Container`"

- [Dockerfiles](#Dockerfiles)
- [MVP-Commands](#MVP-Commands)

## Dockerfiles

- to build the image run (don't forget the . and username & imagename are written small):

`docker build -t USERNAME/IMAGENAME:TAGNAME .`  

- Dockerfiles are build in read-only layers
- ephemeral: stopped, destroyed and reproducible with minimum effort
- current working directory of docker build is called `build context`
- there is only one `CMD` command active, the last one in the file
- `ADD` and `COPY` are similar, but `COPY` is preferred

  - always combine `RUN apt-get update` with `apt-get install -y` in the same `RUN` statement (cache busting)
  - use version pinning where needed, e.g. `3dchess=0.8.1-19`, check the your chosen versions if they (are available)[https://packages.ubuntu.com/search?suite=default&section=all&arch=any&keywords=s3cmd&searchon=names]
  - avoid `RUN apt-get upgrade` or `dist-upgrade`
  - clean up the cache by removing `/var/lib/apt/lists`

```dockerfile
FROM ubuntu:18.04
RUN apt-get update && apt-get install -y \
	curl \
	s3cmd=2.0.* \
	&& rm -rf /var/lib/apt/lists/*
COPY requirements.txt /tmp/
RUN make /app
CMD python /app/app.py
EXPOSE 80/tcp
ENV ADMIN_USER="Manny"
LABEL producer="Manthano"
```

- most common layers:
   - `FROM` creates a layer from an existing docker image | [From-reference](https://docs.docker.com/engine/reference/builder/#from)
   - `COPY` adds files from your Docker client’s current directory | [Copy-reference](https://docs.docker.com/engine/reference/builder/#copy)
   - `RUN` runs something in the shell | [Run-reference](https://docs.docker.com/engine/reference/builder/#run)
   - `CMD` specifies what command to run within the container | [CMD-reference](https://docs.docker.com/engine/reference/builder/#cmd)
   - `LABEL` add one ore more labels | [Label-reference](https://docs.docker.com/engine/reference/builder/#label)
   - `EXPOSE` expose a specific port | (use traditional ports of applications) [Expose-reference](https://docs.docker.com/engine/reference/builder/#expose)
   - `ENV` create environment variables | [Env-reference](https://docs.docker.com/engine/reference/builder/#env)

## MVP-Commands

- [docker run documentation](https://docs.docker.com/engine/reference/commandline/run/)

- run specific container:

   `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`

- run a stopped container:

   `docker start`

- see a list of all containers:

   `docker ps -a`

- delete a specific image:
  - remove by id: `docker rmi IMAGEID`
  - remove by id or name: `docker rm IMAGEID`