# タイムゾーン設定
# Composerコマンドのインストール
# Laravelで必要なPHP拡張機能のインストール
# bcmath, pdo_mysql が不足しているので追加インストール


# ベースとなるDockerコンテナイメージを指定
FROM php:7.3-fpm-alpine
# 生成するイメージのAuthor（作者）を指定
LABEL maintainer "sayaka-tamura"

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

# "RUN, COPY, ADD" 命令が実行されるとイメージのレイヤーが作成
# && \ : LF
RUN set -eux && \
  apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
  cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
  apk del .build-dependencies && \
  docker-php-ext-install bcmath pdo_mysql && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
  composer config -g repos.packagist composer https://packagist.jp && \
  composer global require hirak/prestissimo
