FROM ubuntu:21.04

LABEL maintainer="Marcos Felipe"

# Stop dpkg-reconfigure tzdata from prompting for input
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=UTC

WORKDIR /app

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get install -y gpg zip unzip git gosu openssh-client \
    && mkdir -p ~/.gnupg \
    && chmod 600 ~/.gnupg \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E5267A6C \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C300EE8C \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu hirsute main" > /etc/apt/sources.list.d/ppa_ondrej_php.list \
    && apt-get update -y \
    && apt-get install -y php8.1-cli php8.1-dev \
        php8.1-pgsql php8.1-sqlite3 php8.1-gd \
        php8.1-curl \
        php8.1-imap php8.1-mysql php8.1-mbstring \
        php8.1-xml php8.1-zip php8.1-bcmath php8.1-soap \
        php8.1-intl php8.1-readline \
        php8.1-ldap \
        php8.1-msgpack php8.1-igbinary php8.1-redis php8.1-swoole \
        php8.1-memcached php8.1-pcov php8.1-xdebug \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN groupadd --force -g 1000 sammy \
    && useradd -ms /bin/bash --no-user-group -g 1000 -u 1000 sammy \
    && mkdir -p /home/sammy/.ssh \
    && chown sammy:sammy /home/sammy/.ssh
