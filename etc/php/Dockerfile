FROM alpine:3.7

RUN set -x \
	&& addgroup -g 82 -S www-data \
	&& adduser -u 82 -D -S -G www-data www-data

RUN apk add --no-cache php7 \
    php7-fpm \
    php7-opcache \
    php7-cli \
    php7-mysqli \
    php7-json \
    php7-dom \
    php7-common \
    php7-gd \
    php7-mcrypt \
    php7-curl \
    php7-intl \
    php7-xsl \
    php7-mbstring \
    php7-zip \
    php7-bcmath \
    php7-iconv \
    php7-soap \
    php7-openssl \
    php7-simplexml \
    php7-ctype \
    libxml2-dev \
    php7-pdo \
    php7-phar \
    php7-pdo_mysql \
    php7-xmlwriter \
    php7-cgi \
    php7-tokenizer \
    php7-session \
    php7-xdebug

#
#COPY docker-php-entrypoint /usr/local/bin/
#
#ENTRYPOINT ["docker-php-entrypoint"]

#RUN service php7-fpm restart
#RUN sed -i 's/127.0.0.1:9000/9000/g' /etc/php7/php-fpm.d/www.conf

RUN set -ex \
    && cd /etc/php7 \
	&& { \
		echo '[global]'; \
		echo 'error_log = /proc/self/fd/2'; \
		echo; \
		echo '[www]'; \
		echo '; if we send this to /proc/self/fd/1, it never appears'; \
		echo 'access.log = /proc/self/fd/2'; \
		echo; \
		echo 'clear_env = no'; \
		echo; \
		echo '; Ensure worker stdout and stderr are sent to the main error log.'; \
		echo 'catch_workers_output = yes'; \
	} | tee php-fpm.d/docker.conf \
	&& { \
		echo '[global]'; \
		echo 'daemonize = no'; \
		echo; \
		echo '[www]'; \
		echo 'listen = 9000'; \
	} | tee php-fpm.d/zz-docker.conf

COPY docker-php-entrypoint /usr/local/bin/

ENTRYPOINT ["docker-php-entrypoint"]

ADD php.ini /etc/php7/conf.d/40-custom.ini
ADD xdebug.ini /etc/php7/conf.d/40-xdebug.ini

WORKDIR /var/www/html

EXPOSE 9000

CMD ["php-fpm7"]