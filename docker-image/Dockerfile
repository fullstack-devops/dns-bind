FROM debian:buster-slim

ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL C.UTF-8

###
### Install
###
RUN set -x \
	&& apt-get update \
	&& apt-get install --no-install-recommends --no-install-suggests -y \
		bind9 \
		dnsutils \
		iputils-ping \
	&& apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $fetchDeps \
	&& rm -r /var/lib/apt/lists/* \
	&& mkdir /var/log/named \
	&& chown bind:bind /var/log/named \
	&& chmod 0755 /var/log/named

###
### Bootstrap Scipts
###
COPY ./docker-entrypoint.sh /

###
### Ports
###
EXPOSE 53/udp 53/tcp 953/tcp

####
#### Entrypoint
####
ENTRYPOINT ["/docker-entrypoint.sh"]
