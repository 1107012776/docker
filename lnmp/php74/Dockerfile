FROM php:7.4.12-fpm-alpine3.12

ENV LANG=C.UTF-8
#更新软件和必要库
#php扩展编译需要
#安装扩展
#Install PHP extensions phpredis
ENV REDIS_VERSION=5.3.2
ENV PSR_VERSION=1.0.1
#composer版本
ENV COMPOSER_VERSION=2.0.7
# 删除国外地址 Install env 添加国内镜像到顶部
RUN echo > /etc/apk/repositories \
 && sed -i '1i\http://mirrors.aliyun.com/alpine/v3.12/main/' /etc/apk/repositories \
 && sed -i '1i\http://mirrors.aliyun.com/alpine/v3.12/community/' /etc/apk/repositories
# && sed -i '1i\http://mirrors.ustc.edu.cn/alpine/v3.9/main/' /etc/apk/repositories \
# && sed -i '1i\http://mirrors.ustc.edu.cn/alpine/v3.9/community/' /etc/apk/repositories \
# && sed -i '1i\http://mirrors.aliyun.com/alpine/v3.9/main/' /etc/apk/repositories \
# && sed -i '1i\http://mirrors.aliyun.com/alpine/v3.9/community/' /etc/apk/repositories
#ADD phalcon-pecl.zip /tmp/
RUN  apk add --no-cache  vim jq gmp-dev freetype-dev  libjpeg-turbo-dev libzip-dev  openssl-dev openssh-client gzip \
      linux-headers bash $PHPIZE_DEPS  zip protoc \
  && docker-php-ext-configure gmp \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install bcmath gmp sockets gd  pdo_mysql pcntl opcache \
  && pecl install psr-${PSR_VERSION} && docker-php-ext-enable psr \
  && echo "install psr ok !" \
  && pecl install redis-${REDIS_VERSION} && docker-php-ext-enable redis \
  && echo "install redis ok !" \
  && pecl install zip && docker-php-ext-enable zip \
  && curl -L https://github.com/composer/composer/releases/download/${COMPOSER_VERSION}/composer.phar  -o /usr/local/bin/composer \
  && chmod +x /usr/local/bin/composer \
  && echo -e "disable_functions = phpinfo,eval,passthru,system,chroot,chgrp,chown,shell_exec,ini_alter,ini_alter,ini_restore,dl,pfsockopen,readlink,popepassthru,stream_socket_server,fsocket,fsockopen;\nexpose_php = Off;" > /usr/local/etc/php/conf.d/safety.ini  \
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
