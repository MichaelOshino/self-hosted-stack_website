ARG SITE_PATH=/usr/share/nginx/html
ARG GIT_REPO=https://github.com/MichaelOshino/portfolio-site.git

FROM nginx:alpine AS base

LABEL maintainer="neet@michaeloshino.ru"
LABEL version="3.0"
LABEL description="Сайт портфолио Майкла Ошино"

FROM base AS build

ARG SITE_PATH
ARG GIT_REPO

RUN apk update &&\
    apk add git &&\
    rm -rf $SITE_PATH/* &&\
    git clone $GIT_REPO $SITE_PATH &&\
    rm -rf $SITE_PATH/.git

FROM base AS prod

ARG SITE_PATH

COPY --from=build $SITE_PATH $SITE_PATH
COPY ./default.conf /etc/nginx/templates/default.conf.template

HEALTHCHECK CMD curl -LI http://localhost/ | grep '200 OK' || exit 1