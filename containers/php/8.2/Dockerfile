FROM ubuntu:22.04

LABEL maintainer="Marcos Felipe"

# Stop dpkg-reconfigure tzdata from prompting for input
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=UTC

WORKDIR /app

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && mkdir -p /etc/apt/keyrings \
    && apt-get install -y gnupg gosu curl ca-certificates zip unzip git vim  \
    && mkdir -p ~/.gnupg \
    && chmod 600 ~/.gnupg \
    && curl -sS 'https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x14aa40ec0831756756d7f66c4f4ea0aae5267a6c' | gpg --dearmor | tee /etc/apt/keyrings/ppa_ondrej_php.gpg > /dev/null \
    && echo "deb [signed-by=/etc/apt/keyrings/ppa_ondrej_php.gpg] https://ppa.launchpadcontent.net/ondrej/php/ubuntu jammy main" > /etc/apt/sources.list.d/ppa_ondrej_php.list \
    && apt-get update -y \
    && apt-get install -y php8.2-cli php8.2-dev \
        php8.2-pgsql php8.2-sqlite3 php8.2-gd \
        php8.2-curl \
        php8.2-imap php8.2-mysql php8.2-mbstring \
        php8.2-xml php8.2-zip php8.2-bcmath php8.2-soap \
        php8.2-intl php8.2-readline \
        php8.2-ldap \
        php8.2-msgpack php8.2-igbinary php8.2-redis php8.2-swoole \
        php8.2-memcached php8.2-pcov php8.2-xdebug \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN groupadd --force -g 1000 sammy \
    && useradd -ms /bin/bash --no-user-group -g 1000 -u 1000 sammy \
    && mkdir -p /home/sammy/.ssh \
    && chown sammy:sammy /home/sammy/.ssh
