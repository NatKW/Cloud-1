FROM alpine:3.15

RUN apk update && apk upgrade && apk add --no-cache mariadb \
    mariadb-client

COPY /tmp/mariadb/configure.sh /configure.sh

EXPOSE 3306

ENTRYPOINT ["sh", "configure.sh"]