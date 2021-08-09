FROM php:5.6-fpm-alpine3.8

ENV LANG=C.UTF-8
#更新软件和必要库
#php扩展编译需要
#安装扩展
ENV REDIS_VERSION=4.2.0
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
  && apk update --no-cache  \
  && apk add --no-cache vim jq gmp-dev freetype-dev  libjpeg-turbo-dev libzip-dev libmcrypt-dev openssl-dev openssh-client yaml-dev gzip \
     protobuf-dev linux-headers bash $PHPIZE_DEPS  zip  \
  && docker-php-ext-configure gmp \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && apk update \
  && docker-php-ext-install bcmath gmp sockets gd pdo_mysql mcrypt pcntl opcache \
  && pecl install redis-${REDIS_VERSION} && docker-php-ext-enable redis \
  && echo "install redis ok !" \
  && pecl install zip && docker-php-ext-enable zip \
  && pecl clear-cache && apk del $PHPIZE_DEPS  \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apk/* \
           /usr/share/doc/* /name/usr/share/man/* /usr/share/info/* \
  && sed -i 's#root:x:0:0:root:/root:/bin/ash#root:x:0:0:root:/root:/bin/bash#g' /etc/passwd


#卸载phpize-deps
#清理缓存
#core dump test
#RUN echo '/tmp/core.%p' > /proc/sys/kernel/core_pattern
#RUN apt-get install -y gdb
WORKDIR /data/www
