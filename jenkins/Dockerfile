FROM jenkins/jenkins:lts

LABEL version="0.0.1"
LABEL description="Jenkins with additional packages for test environment"

USER root

RUN apt-get update && \
    apt-get install -qqy --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    software-properties-common \
    qemu-kvm \
    qemu-utils

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

RUN apt-get update && \
    apt-get install -qqy --no-install-recommends docker-ce

RUN apt-get clean && \
    apt-get autoremove -y

RUN rm -rf /var/lib/apt/lists/*

RUN usermod -aG docker jenkins

USER jenkins

# vim: ts=4 sw=4 et
