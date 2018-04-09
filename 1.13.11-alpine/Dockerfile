FROM nginx:1.13.11-alpine

RUN adduser -u 5000 -S otrs \
    && addgroup -g 5000 -S otrs

COPY default.conf /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/nginx.conf
