FROM php:7.2.33-fpm-alpine3.12

#分配Hugepages(设置在宿主机上设置即可)
# RUN sysctl  vm.nr_hugepages=128

#RUN echo "memory_limit = 256M;" >> /usr/local/etc/php/php.ini
ENV LANG=C.UTF-8
#更新软件和必要库
#php扩展编译需要
#安装扩展
#Install PHP extensions phpredis
ENV REDIS_VERSION=5.3.1


# xdebug apk add py-pygraphviz python
# 删除国外地址 Install env 添加国内镜像到顶部
RUN  echo > /etc/apk/repositories \
# && sed -i '1i\http://mirrors.ustc.edu.cn/alpine/v3.9/main/' /etc/apk/repositories \
# && sed -i '1i\http://mirrors.ustc.edu.cn/alpine/v3.9/community/' /etc/apk/repositories \
 && sed -i '1i\http://mirrors.aliyun.com/alpine/v3.12/main/' /etc/apk/repositories \
 && sed -i '1i\http://mirrors.aliyun.com/alpine/v3.12/community/' /etc/apk/repositories 
RUN  apk add --no-cache  vim jq gmp-dev freetype-dev  libjpeg-turbo-dev libzip-dev  openssl-dev openssh-client gzip \
      linux-headers bash $PHPIZE_DEPS  zip  \
  && docker-php-ext-configure gmp \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/freetype2 --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-configure zip \
  && docker-php-ext-install bcmath gmp sockets gd  pdo_mysql pcntl opcache zip \
  && pecl install redis-${REDIS_VERSION} && docker-php-ext-enable redis \
  && echo "install redis ok !" \
# && pecl install zip && docker-php-ext-enable zip \
  && echo -e "disable_functions = eval,passthru,system,chroot,chgrp,chown,shell_exec,ini_alter,ini_alter,ini_restore,dl,pfsockopen,readlink,symlink,popepassthru,stream_socket_server,fsocket,fsockopen;\nexpose_php = Off;" > /usr/local/etc/php/conf.d/safety.ini  \
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