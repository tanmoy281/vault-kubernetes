FROM alpine:3.10

ARG VAULT_VERSION=1.3.0
ARG ARCH=arm64

RUN apk update && \
    apk add vim && \
    apk add supervisor && \
	apk add bash

# vault release version 0.10.1 - copy vault binary
#COPY vault /usr/local/bin/vault

COPY vault.cfg /usr/local/bin/vault.cfg

ADD supervisor.conf /etc/supervisor.conf

#add group vault and user vault
RUN addgroup vault && \
    adduser -S -G vault vault && \
    mkdir -p /vault/logs && \
    mkdir -p /vault/config && \
    chown -R vault:vault /vault && \
    chown -R vault:vault /usr/local/bin  && \
    chown -R vault:vault /var/log && \
	mkdir -p /etc/supervisor/conf.d && \
    chown -R vault:vault /etc/supervisor && \
    mkdir -p /var/log/supervisor  && \
	chown -R vault:vault /var/log/supervisor &&\
	mkdir -p /tmp/build && \
    cd /tmp/build && \
    wget https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_${ARCH}.zip && \
    unzip -d /usr/local/bin vault_${VAULT_VERSION}_linux_${ARCH}.zip && \
	cd /tmp && \
    rm -rf /tmp/build


# Expose the logs directory as a volume since there's potentially long-running
VOLUME /vault/logs

EXPOSE 8200

USER vault

WORKDIR /usr/local/bin

CMD ["supervisord", "-c", "/etc/supervisor.conf"]