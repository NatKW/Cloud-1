FROM	alpine:3.15

RUN	apk update && apk upgrade && apk add --no-cache \
    wget vim tar openssl \
	php7 php7-fpm php7-opcache \
	php7 php7-cli php7-fpm php7-json \
	php7-common php7-mysqli php7-zip \
	php7-gd php7-mbstring php7-xml php7-phar\
	php7-xml php7-pear php7-openssl php7-bcmath
RUN rm -rf /var/cache/apk/*

RUN	adduser -S nginx &&	addgroup -S nginx

RUN wget https://files.phpmyadmin.net/phpMyAdmin/5.2.0/phpMyAdmin-5.2.0-english.tar.gz -O /tmp/phpMyAdmin.tar.gz
RUN tar -xvzf /tmp/phpMyAdmin.tar.gz -C /tmp
RUN mkdir -p /var/www/html/phpmyadmin
RUN mkdir /var/www/html//phpmyadmin/tmp && chmod 0777 /var/www/html//phpmyadmin/tmp
RUN cp -r /tmp/phpMyAdmin-5.2.0-english/* /var/www/html/phpmyadmin

COPY ./config.inc.php /var/www/html/phpmyadminconfig.inc.php
RUN	echo "\$cfg['blowfish_secret'] = '$(openssl rand -base64 32)';" >> /var/www/html/config.inc.php

RUN sed -i 's/listen = \/run\/php\/php7.4-fpm.sock/listen = 8888/g' /etc/php7/php-fpm.d/www.conf
RUN mkdir /run/php7/
RUN touch /var/log/php7/error.log \
	&& chmod a+rwx /var/log/php7/error.log
RUN chown -R nginx:nginx /var/www/html//phpmyadmin/index.php /run/php7 /var/log/php7/error.log

USER nginx

EXPOSE 8888

ENTRYPOINT [ "php-fpm7", "--nodaemonize" ]