# Docker :whale: 

"`Dockerfile` builds `Image` runs `Container`"

- [Dockerfiles](#Dockerfiles)
- [MVP-Commands](#MVP-Commands)

## Dockerfiles

- To build the image run `docker build -t USERNAME/IMAGENAME:TAGNAME .` (don't forget the . , username, imagename, tagname written small)

- Dockerfiles are build in read-only layers
- Ephemeral, stopped, destroyed and reproducible with minimum effort
- Current working directory of docker build is called `build context`
- Always combine `RUN apt-get update` with `apt-get install -y` in the same `RUN` statement (cache busting)
- Use version pinning where needed, e.g. `s3cmd=1.1*`
- Avoid `RUN apt-get upgrade` or `dist-upgrade`
- Clean up the cache by removing `/var/lib/apt/lists`
- There is only one `CMD` command active, the last one in the file
- `ADD` and `COPY` are similar, but `COPY` is preferred

```dockerfile
FROM ubuntu:18.04
RUN apt-get update && apt-get install -y \
	curl \
	s3cmd=2.1.* \
	&& rm -rf /var/lib/apt/lists/*
COPY requirements.txt /tmp/
RUN make /app
CMD python /app/app.py
EXPOSE 80/tcp
ENV ADMIN_USER="Manny"
LABEL producer="Manthano"
```

- Most common layers:
   - `FROM` creates a layer from the ubuntu:18.04 Docker image | [From-reference](https://docs.docker.com/engine/reference/builder/#from)
   - `COPY` adds files from your Docker client’s current directory [Copy-reference](https://docs.docker.com/engine/reference/builder/#copy)
   - `RUN` builds your application with make [Run-reference](https://docs.docker.com/engine/reference/builder/#run)
   - `CMD` specifies what command to run within the container [CMD-reference](https://docs.docker.com/engine/reference/builder/#cmd)
   - `LABEL` add one ore more labels [Label-reference](https://docs.docker.com/engine/reference/builder/#label)
   - `EXPOSE` expose a specific port (use traditional ports of applications) [Expose-reference](https://docs.docker.com/engine/reference/builder/#expose)
   - `ENV` create environment variables [Env-reference](https://docs.docker.com/engine/reference/builder/#env)

## MVP-Commands

- run specific container:

   `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`

- run a stopped container:

   `docker start`

- see a list of all containers:

   `docker ps -a`

- [full documentation](https://docs.docker.com/engine/reference/commandline/run/)
