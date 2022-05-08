ARG JENKINS_VERSION=2.332.1
FROM jenkins/jenkins:${JENKINS_VERSION}-jdk11

USER root
ARG DOCKER_VERSION=20.10.12
RUN curl -fsSL https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz \
    | tar -xzv \
 && mv docker/docker /usr/local/bin/ \
 && chmod +x /usr/local/bin/docker \
 && rm -rf docker

COPY awscliv2.pub ./
ARG AWS_CLI_VERSION=2.4.16
RUN set -x \
 && curl -o awscliv2.zip "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-${AWS_CLI_VERSION}.zip" \
 && curl -o awscliv2.sig "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-${AWS_CLI_VERSION}.zip.sig" \
 && gpg --import awscliv2.pub \
 ;  gpg --verify awscliv2.sig awscliv2.zip \
 && unzip awscliv2.zip \
 && ./aws/install \
    --bin-dir /usr/local/bin \
    --install-dir /usr/local/aws-cli \
 && rm -rf awscliv2.* ./aws

USER jenkins