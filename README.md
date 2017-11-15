# Jenkins With Docker

This is a simple dockerfile that pulls from the [Jenkins Docker Image](https://hub.docker.com/r/jenkins/jenkins/), adds in [Docker CE](https://docs.docker.com/) for the command line interface, and sets up the user account for the shared docker socket from [CoreOS](https://coreos.com/).

### Supported tags and respective `Dockerfile` links

- [`latest`](https://github.com/coodeneko/jenkins-with-docker/blob/master/Dockerfile)
- [`lts`](https://github.com/coodeneko/jenkins-with-docker/blob/master/lts/Dockerfile)
- [`alpine`](https://github.com/coodeneko/jenkins-with-docker/blob/master/alpine/Dockerfile)
- [`lts-alpine`](https://github.com/coodeneko/jenkins-with-docker/blob/master/lts/alpine/Dockerfile)
- [`slim`](https://github.com/coodeneko/jenkins-with-docker/blob/master/slim/Dockerfile)
- [`lts-slim`](https://github.com/coodeneko/jenkins-with-docker/blob/master/lts/slim/Dockerfile)

### Usage

Template Systemd Service Unit using port 8080

```
[Unit]
Description=Jenkins container
Author=Kreutzwieser Joel
After=docker.service

[Service]
Restart=always
ExecStartPre=-/usr/bin/docker kill jenkins
ExecStartPre=-/usr/bin/docker rm jenkins
ExecStartPre=/usr/bin/docker pull codeneko/jenkins-with-docker
ExecStart=/usr/bin/docker run --rm -p 8080:8080 -p 50000:50000 -v /home/jenkins:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins codeneko/jenkins-with-docker
ExecStop=/usr/bin/docker stop jenkins
```