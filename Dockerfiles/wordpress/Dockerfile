FROM	alpine:3.15
RUN		apk update && apk upgrade && apk add --no-cache \
		mariadb-client \
		wget \
		vim \
		php7-cli php7-gd php7-mysqli	
RUN		rm -rf /var/lib/apt/lists/*

RUN 	sed -i 's/listen = \/run\/php7\/php-fpm7.sock/listen = 9000/g' /etc/php7/php-fpm.d/www.conf

#Download and Setup Worpress-cli https://wp-cli.org/fr/
RUN 	wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar -O /tmp/wp-cli.phar
RUN 	chmod +x /tmp/wp-cli.phar
RUN		mv /tmp/wp-cli.phar /usr/bin/wp
RUN		chown -R nginx:nginx /usr/bin/wp /var/www/html/

WORKDIR /var/www/html/
COPY /start.sh start.sh

ENTRYPOINT [ "sh", "/start.sh" ]
