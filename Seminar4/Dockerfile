FROM alpine:3.4

VOLUME /var/lib/mysql

RUN apk update \
    && apk add mariadb mariadb-client gnupg \
    && mkdir -p /var/lib/mysql /var/run/mysqld \
    && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
    && chmod 777 /var/run/mysqld \
    && mysql_install_db --user=mysql

EXPOSE 3306

COPY users.sql /

ENTRYPOINT ["mysqld_safe","--user","mysql"]