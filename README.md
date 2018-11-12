build the binary using:

```bash
docker build . && \
docker run -v <PATH TO SOURCES>:/sources/crashdump --env CGO_ENABLED=0
```

run the build using:

```bash
docker build -f Dockerfile.run . && \
docker run -p 8080:8080 -v <PATH TO SOURCES>:/sources/crashdump --env GOTRACEBACK=crash --cap-add="SYS_PTRACE" --security-opt="apparmor=unconfined"
```

to get a dump run:

```bash
docker exec -it <CONTAINER ID> /bin/bash
```
and then inside the container, run:
```bash
gcore -o core.dmp 1
```