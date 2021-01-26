# Docker :whale: :whale: :whale:

## Dockerfiles

- Dockerfiles are build in read-only layers
- Ephemeral, stopped, destroyed and reproducible with minimum effort

```dockerfile
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

- Most common layers:
   - `FROM` creates a layer from the ubuntu:18.04 Docker image.
   - `COPY` adds files from your Docker client’s current directory
   - `RUN` builds your application with make
   - `CMD` specifies what command to run within the container
