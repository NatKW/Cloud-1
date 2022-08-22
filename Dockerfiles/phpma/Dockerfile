FROM	alpine:3.15
RUN	apk update && apk upgrade && apk add --no-cache \
    wget \
	php7 php7-cli php7-fpm php7-json \
	php7-common php7-mysqli php7-zip \
	php7-gd php7-mbstring php7-xml php-phar\
	php7-xml php7-pear php7-openssl php7-bcmath 
RUN rm -rf /var/cache/apk/*

# Php config
RUN	adduser -S nginx &&	addgroup -S nginx
COPY	tools/php-fpm.conf /etc/php7/php-fpm.conf
COPY	tools/www.conf /etc/php7/php-fpm.d/www.conf
RUN     mkdir -p /var/www/html/
RUN 	chmod 777 /var/www/html/

ENTRYPOINT [ "sh", "/tmp/configure.sh" ]