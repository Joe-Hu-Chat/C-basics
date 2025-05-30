# Docker learning

ref: https://vuepress.mirror.docker-practice.com/appendix/best_practices/#label

ref: https://github.com/yeasy/docker_practice/tree/master

Since the Docker Hub `hub.docker.com` is fully banned in China, it would be practical to build docker image from scratch.
Here are some sources:

Historical debian version:
https://github.com/debuerreotype/docker-debian-eol-artifacts/tree/dist-squeeze
Stable version of debian docker:
https://github.com/debuerreotype/docker-debian-artifacts/blob/ba01688d8eb18826b9ea238a8f9c98ec92eedc60/stable/Dockerfile

See especially the `dist-*` branches, such as *dist-squeeze*'s *squeeze* directory.



## Command

More commonly used docker commands:
**build**: `docker build -t my-docker .`
This command will build a docker image "my-docker" based on the `Dockerfile` in .(current directory).

**run**: `docker run -it my-docker`
This command will run the docker image "my-docker" in an interactive way in a `tty`.

**exit**: `exit`
We use this command to quit the container.

**mount**: `docker run -it --mount type=bind,source=/media/joe/SPEC_CPU2006v1.2,target=/mnt my-debian-docker`

This option mounts a host directory (`/media/joe/SPEC_CPU2006v1.2`) to container (`/mnt`).

`docker run -it --mount type=bind,source=/media/joe/SPEC_CPU2006v1.2,target=/mnt --mount type=bind,source=/home/joe/spec2006,target=/root my-debian-docker`  # Mount multiple directories to a docker.



## Dockerfile


A Dockerfile to build SPEC2006 environment on debian squeeze is like:
```dockerfile
FROM scrach
ADD rootfs.tar.xz /
RUN apt-get update && apt-get install -y build-essential \
gfortran \
p7zip-full
CMD ["bash"]
```
