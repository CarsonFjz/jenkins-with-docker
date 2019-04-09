FROM jenkins/jenkins:lts
USER root
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common \
    && curl -fsL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add - \
    && apt-key fingerprint 0EBFCD88 \
    && add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
        $(lsb_release -cs) \
        stable" \
    && apt-get update \
    && curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash \
    && apt-get install -y docker-ce git-lfs \
    && git lfs install \
    && groupmod -g 233 docker && usermod -a -G docker jenkins \
    && curl -L https://github.com/docker/compose/releases/download/1.8.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose
USER jenkins
