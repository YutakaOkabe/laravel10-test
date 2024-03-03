FROM php:8.2-apache

ARG WWW_USER_ID=${WWW_USER_ID}
ARG WWW_GROUP_ID=${WWW_GROUP_ID}

RUN apt update && apt install -y zlib1g-dev g++ libicu-dev zip libzip-dev zip libpq-dev \
    # mysqlの場合
    # && docker-php-ext-install intl opcache pdo pdo_mysql \
    # mysqlの場合
    && docker-php-ext-install intl opcache pdo pgsql pdo_pgsql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && apt-get install -y git \
    && a2enmod rewrite

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# node
RUN apt-get install -y nodejs npm && npm install n -g && n 18.16.0

# php.ini設置
COPY ./php.ini /usr/local/etc/php/
# apache設定ファイル設置
COPY ./conf/000-default.conf /etc/apache2/sites-available/000-default.conf

# コンテナ内に名称dockerでグループを作成
RUN groupadd -g ${WWW_GROUP_ID} docker
# コンテナ内に名称dockerでdockerグループに所属するユーザーを作成
RUN useradd -u ${WWW_USER_ID} -g ${WWW_GROUP_ID} -s /bin/bash -m docker
# コンテナを実行するユーザーを指定
USER ${WWW_USER_ID}

WORKDIR /var/www/html
