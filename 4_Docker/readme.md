# Docker :whale:

## Dockerfiles

- Dockerfiles are build in read-only layers
- Ephemeral, stopped, destroyed and reproducible with minimum effort
- Current working directory of docker build is called `build context`
- To build the image run `docker build .` (don't forget the .)
- Always combine `RUN apt-get update` with `apt-get install -y` in the same `RUN` statement (cache busting)
- Use version pinning where needed, e.g. `s3cmd=1.1*`
- Avoid `RUN apt-get upgrade` or `dist-upgrade`
- Clean up the cache by removing `/var/lib/apt/lists`

```dockerfile
FROM ubuntu:18.04
RUN apt-get update && apt-get install -y \
	curl \
	s3cmd=1.1* \
	&& rm -rf /var/lib/apt/lists/*
COPY . /app
RUN make /app
CMD python /app/app.py
LABEL producer="Manthano"
```

- Most common layers:
   - `FROM` creates a layer from the ubuntu:18.04 Docker image.
   - `COPY` adds files from your Docker client’s current directory
   - `RUN` builds your application with make
   - `CMD` specifies what command to run within the container
   - `LABEL` add one ore more labels

## RUN