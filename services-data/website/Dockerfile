FROM nginx:alpine AS base

LABEL maintainer="neet@michaeloshino.ru"
LABEL version="2.0"
LABEL description="Сайт портфолио Майкла Ошино"

ENV SITE_PATH=/usr/share/nginx/html

FROM base AS build

RUN apk update &&\
    apk add git &&\
    rm -rf $SITE_PATH/* &&\
    git clone https://github.com/MichaelOshino/portfolio-site.git $SITE_PATH &&\
    rm -rf $SITE_PATH/.git

FROM base AS prod

COPY --from=build $SITE_PATH $SITE_PATH
COPY ./default.conf /etc/nginx/templates/default.conf.template

HEALTHCHECK CMD curl -LI --fail http://localhost:${WEBSITE_PORT}/ | grep '200 OK' || exit 1