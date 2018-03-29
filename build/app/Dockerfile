FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
        curl \
        software-properties-common && \
    LC_ALL=C.UTF-8 add-apt-repository -y -u ppa:ondrej/php && \
    curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata && \
    ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    dpkg-reconfigure --frontend noninteractive tzdata && \
    apt-get install -y \
        php7.1-fpm \
        php7.1-xdebug \
        php7.1-phalcon

ARG AGENT_UID=1000
RUN adduser --quiet --disabled-login --disabled-password --shell /bin/sh --uid ${AGENT_UID} apache

COPY php.ini /etc/php.ini
COPY 20-xdebug.ini /etc/php/7.1/fpm/conf.d/20-xdebug.ini
COPY php-fpm.conf /etc/php-fpm.conf
#COPY php-fpm.conf /etc/php-fpm.d/www.conf
RUN mkdir -p /run/php

ENV PATH /usr/sbin:$PATH
EXPOSE 9000
CMD ["php-fpm7.1", "-F", "-y", "/etc/php-fpm.conf"]
#CMD ["php-fpm7.1", "-F"]
