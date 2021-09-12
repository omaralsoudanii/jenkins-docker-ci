FROM jenkins/jenkins:lts-jdk11

ENV DOCKER_TLS_VERIFY 1
ENV DOCKER_CERT_PATH /certs/client
ENV DOCKER_HOST tcp://docker:2376
# https://www.jenkins.io/doc/book/installing/docker/#setup-wizard
# with root install docker stuff for docker:dind image
USER root
RUN apt-get update && apt-get install -y apt-transport-https \
       ca-certificates curl gnupg2 \
       software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce-cli

RUN curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
# run jenkins with blueocean and docker-workflow plugins installed non-root mode
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean:1.24.8 docker-workflow:1.26"