# 基础
FROM php:5.6-fpm

# 有 /etc/apt/sources.list

#deb http://deb.debian.org/debian stretch main
#deb http://security.debian.org/debian-security stretch/updates main
#deb http://deb.debian.org/debian stretch-updates main
#
# 没有 /etc/apk/repositories

#  设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN     mv /etc/apt/sources.list  /etc/apt/sources.list.bak \
        && echo 'deb [trusted=yes] http://mirrors.ustc.edu.cn/debian stable main contrib non-free' >> /etc/apt/sources.list \
        && echo 'deb [trusted=yes] http://mirrors.ustc.edu.cn/debian stable-updates main contrib non-free' >> /etc/apt/sources.list \
        && apt-get update \
        && apt-get install vim -y \
        && apt-get install wget -y \
        && mkdir /usr/include/freetype \
        && wget -O /usr/include/freetype/freetype-2.8.tar.gz https://mirror.ossplanet.net/nongnu/freetype/freetype-2.8.tar.gz \
        && cd /usr/include/freetype/ \
        && tar -zxf freetype-2.8.tar.gz \
        && cd freetype-2.8 \
        && ./configure --prefix=/usr/include/freetype && make && make install \
        && apt-get install libjpeg-dev -y \
        && apt-get install libpng-dev -y \
        && apt-get install libfontconfig1-dev -y \
        && docker-php-ext-configure gd   --with-freetype-dir=/usr/include/freetype  --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ && docker-php-ext-install -j$(nproc) gd \
        && docker-php-ext-install zip \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install opcache \
        && docker-php-ext-install mysqli \
        && pecl install xdebug-2.5.5 \
        && docker-php-ext-enable xdebug \
        && no | pecl install redis-4.0.1 \
        && docker-php-ext-enable redis \
        && rm -r /var/lib/apt/lists/*