FROM alpine:3.8

RUN apk add --update nginx && rm -rf /var/cache/apk/*

COPY default.conf /etc/nginx/conf.d/default.conf

RUN mkdir -p /run/nginx

COPY docker-nginx-entrypoint /usr/local/bin/

ENTRYPOINT ["docker-nginx-entrypoint"]

EXPOSE 9000

CMD ["nginx", "-g", "daemon off;"]