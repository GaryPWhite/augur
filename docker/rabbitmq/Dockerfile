FROM rabbitmq:3.12-management-alpine

LABEL maintainer="574/augur@simplelogin.com"
LABEL version="0.63.3"

ARG RABBIT_MQ_DEFAULT_USER
ARG RABBIT_MQ_DEFAULT_PASSWORD
ARG RABBIT_MQ_DEFAULT_VHOST

COPY --chown=rabbitmq:rabbitmq ./docker/rabbitmq/augur.conf /etc/rabbitmq/conf.d/

ADD docker/rabbitmq/definitions.json /etc/rabbitmq/
RUN chown rabbitmq:rabbitmq /etc/rabbitmq/definitions.json

ADD docker/rabbitmq/advanced.config /etc/rabbitmq/
RUN chown rabbitmq:rabbitmq /etc/rabbitmq/advanced.config

RUN chmod 777 /etc/rabbitmq/conf.d/augur.conf

RUN apk add --no-cache python3
COPY docker/rabbitmq/update_config.py /

RUN exec python3 update_config.py