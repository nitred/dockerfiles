# About
This repository contains Dockerfiles for different projects.

# Notes

## X-server compatibility

#### Dockerfile
```
# creating a user named developer
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends sudo && \
    rm -rf /var/lib/apt/lists/* && \
    export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

USER developer
ENV HOME /home/developer
WORKDIR "/home/developer"
```

#### Docker Run Command
```
sudo docker run \
            --name <CONTAINER_NAME> \
            -e DISPLAY=$DISPLAY \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -t -i <IMAGE_NAME> /bin/bash
```
