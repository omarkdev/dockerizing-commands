FROM ubuntu:21.04

LABEL maintainer="Marcos Felipe"

# Stop dpkg-reconfigure tzdata from prompting for input
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=UTC

WORKDIR /app

RUN apt-get update \
    && apt-get install -y gpg zip unzip git gosu openssh-client curl python2 \
    && curl -fsSL --silent https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get install -y nodejs \
    && apt-get install -y build-essential \
    && npm i -g yarn

RUN groupadd --force -g 1000 sammy \
    && useradd -ms /bin/bash --no-user-group -g 1000 -u 1000 sammy \
    && mkdir -p /home/sammy/.ssh \
    && chown sammy:sammy /home/sammy/.ssh
