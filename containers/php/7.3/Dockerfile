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
    && apt-get install -y php7.3-cli php7.3-dev \
        php7.3-pgsql php7.3-sqlite3 php7.3-gd \
        php7.3-curl \
        php7.3-imap php7.3-mysql php7.3-mbstring \
        php7.3-xml php7.3-zip php7.3-bcmath php7.3-soap \
        php7.3-intl php7.3-readline \
        php7.3-ldap \
        php7.3-msgpack php7.3-igbinary php7.3-redis php7.3-swoole \
        php7.3-memcached php7.3-pcov php7.3-xdebug \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN groupadd --force -g 1000 sammy \
    && useradd -ms /bin/bash --no-user-group -g 1000 -u 1000 sammy \
    && mkdir -p /home/sammy/.ssh \
    && chown sammy:sammy /home/sammy/.ssh
