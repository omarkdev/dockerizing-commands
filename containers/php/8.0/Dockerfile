FROM ubuntu:21.10

LABEL maintainer="Marcos Felipe"

# Stop dpkg-reconfigure tzdata from prompting for input
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=UTC

WORKDIR /app

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get install -y gpg zip unzip git gosu openssh-client libcap2-bin \
    && mkdir -p ~/.gnupg \
    && chmod 600 ~/.gnupg \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E5267A6C \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C300EE8C \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu impish main" > /etc/apt/sources.list.d/ppa_ondrej_php.list \
    && apt-get update -y \
    && apt-get install -y php8.0-cli php8.0-dev \
        php8.0-pgsql php8.0-sqlite3 php8.0-gd \
        php8.0-curl php8.0-memcached \
        php8.0-imap php8.0-mysql php8.0-mbstring \
        php8.0-xml php8.0-zip php8.0-bcmath php8.0-soap \
        php8.0-intl php8.0-readline php8.0-pcov \
        php8.0-ldap \
        php8.0-msgpack php8.0-igbinary php8.0-redis php8.0-swoole \
        php8.0-xdebug \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN update-alternatives --set php /usr/bin/php8.0
RUN setcap "cap_net_bind_service=+ep" /usr/bin/php8.0

RUN groupadd --force -g 1000 sammy \
    && useradd -ms /bin/bash --no-user-group -g 1000 -u 1000 sammy \
    && mkdir -p /home/sammy/.ssh \
    && chown sammy:sammy /home/sammy/.ssh
