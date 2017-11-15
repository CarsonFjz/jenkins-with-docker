FROM jenkins/jenkins:alpine
USER root
RUN apk add --no-cache docker \
    && delgroup docker && addgroup -g 233 docker && addgroup jenkins docker
USER jenkins