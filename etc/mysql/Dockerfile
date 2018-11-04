FROM alpine:latest

WORKDIR /var/lib/mysql

VOLUME /var/lib/mysql

RUN apk add --update mysql mysql-client && rm -f /var/cache/apk/*

COPY startup.sh /startup.sh
COPY my.cnf /etc/mysql/my.cnf

RUN chmod +x /startup.sh
RUN chmod 0444 /etc/mysql/my.cnf

EXPOSE 3306

CMD ["/startup.sh"]