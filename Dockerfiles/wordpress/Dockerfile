FROM	alpine:3.15
RUN		apk update && apk upgrade && apk add --no-cache \
		mariadb-client \
		wget \
		vim \
RUN 	echo "http://dl-cdn.alpinelinux.org/alpine/v3.15/main" >> /etc/apk/repositories \
    	&& apk add --no-cache php7 php7-fpm php7-opcache \
		php7-cli php7-gd php7-mysqli
	
RUN	rm -rf /var/lib/apt/lists/*

# Php config
RUN 	mkdir /run/php
RUN 	sed '/^listen =/s/\/run\/php\/php7.4-fpm.sock/9000/' -i /etc/php/7.4/fpm/pool.d/www.conf
RUN		adduser -S nginx &&	addgroup -S nginx

RUN     mkdir -p /var/www/html/
RUN 	chmod 777 /var/www/html/

#Download and Setup Worpress-cli https://wp-cli.org/fr/
RUN 	wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN		php wp-cli.phar --info
RUN 	chmod +x wp-cli.phar
RUN		mv wp-cli.phar /usr/bin/wp
RUN		chown -R nginx:nginx /usr/bin/wp /var/www/html/

WORKDIR /var/www/html/
COPY /start.sh /start.sh

ENTRYPOINT [ "sh", "/start.sh" ]
