FROM nginx:alpine

LABEL maintainer="neet@michaeloshino.ru"
LABEL version="1.0"
LABEL description="Сайт портфолио Майкла Ошино"

COPY ./default.conf /etc/nginx/templates/default.conf.template
RUN apk update &&\
    apk add git &&\
    git clone https://github.com/MichaelOshino/portfolio-site.git &&\
    rm -rf /usr/share/nginx/html/* &&\
    mv ./portfolio-site/* /usr/share/nginx/html/ &&\
    rm -rf ./portfolio-site

HEALTHCHECK CMD curl -LI --fail http://localhost:${WEBSITE_PORT}/ | grep '200 OK' || exit 1