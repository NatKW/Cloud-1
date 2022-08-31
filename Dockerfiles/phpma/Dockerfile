FROM	alpine:3.15

RUN	apk update && apk upgrade && apk add --no-cache \
    wget vim tar \
	php7 php7-cli php7-fpm php7-json \
	php7-common php7-mysqli php7-zip \
	php7-gd php7-mbstring php7-xml php7-phar\
	php7-xml php7-pear php7-openssl php7-bcmath 
RUN wget -q https://files.phpmyadmin.net/phpMyAdmin/5.2.0/phpMyAdmin-5.2.0-english.tar.gz -O /tmp/phpmyadmin.tar.gz
RUN rm -rf /var/cache/apk/*

RUN mkdir -p /var/www/phpmyadmin
RUN tar -zxf /tmp/phpmyadmin.tar.gz -C /tmp
RUN mkdir /var/www/phpmyadmin/tmp && chmod 0777 /var/www/phpmyadmin/tmp
RUN cp -r /tmp/phpMyAdmin-5.2.0-english/* /var/www/phpmyadmin
RUN cp /var/www/phpmyadmin/config.sample.inc.php /var/www/phpmyadmin/config.inc.php
RUN sed -i 's/localhost/mysql/g' /var/www/phpmyadmin/config.inc.php
RUN echo >> /var/www/phpmyadmin/config.inc.php
RUN echo "\$cfg['blowfish_secret'] = '$(openssl rand -base64 32)';" >> /var/www/phpmyadmin/config.inc.php
RUN adduser -S nginx &&	addgroup -S nginx

COPY ./index.php /var/www/phpmyadmin/index.php

RUN mkdir /run/php/
RUN chown -R nginx:nginx /var/www/phpmyadmin /run/php

USER nginx

ENTRYPOINT [ "php-fpm7", "--nodaemonize" ]