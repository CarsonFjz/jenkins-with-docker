# Jenkins With Docker

This is a simple dockerfile that pulls from the [Jenkins LTS Docker Image](https://hub.docker.com/r/jenkins/jenkins/), adds in [Docker CE](https://docs.docker.com/engine/installation/linux/docker-ce/debian/) for the command line interface, and sets up the user account for the shared docker socket from [CoreOS](https://coreos.com/).

## Usage

Template Systemd Service Unit

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