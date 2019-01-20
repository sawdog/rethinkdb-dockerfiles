FROM alpine:3.8
MAINTAINER Andrew Sawyers <andrew@sawdog.com>

COPY ./conf/default.conf /etc/rebirthdb/default.conf

ENV LANG en_US.utf8


RUN set -ex \
	\
	&& apk add --no-cache --virtual .fetch-deps \
		bash

#RUN apt-get update \
#    && apt-get install -y bash wget gnupg2

SHELL ["/bin/bash", "-c"]

# Add the rethinkdb repository and public key
# There is currently no public repor; so at present Packaging is currently borked; can't grab the deb from the -dev repo
#RUN source /etc/lsb-release \
# && echo "deb [trusted=yes] https://foo.bar.com/rethinkdb-dev/apt $DISTRIB_CODENAME main" | tee /etc/apt/sources.list.d/rethinkdb.list \
# && echo "deb [trusted=yes] https://foo.bar.com/rethinkdb/apt $DISTRIB_CODENAME main" | tee /etc/apt/sources.list.d/rethinkdb.list \
#    && wget -qO- https://foo.bar.com/rethinkdb/keys/pubkey.gpg | apt-key add - \
#    && apt-get update \
#    && apt-get install -y rethinkdb

# we have to install from locally stored deb as a temp workaround
WORKDIR /tmp
COPY ./deb/rethinkdb_2.3.6.srh.1.0bionic_amd64.deb ./rethinkdb_2.3.6-bionic_amd64.deb
RUN apt install -y ./rethinkdb_2.3.6-bionic_amd64.deb \
    && rm ./rethinkdb_2.3.6-bionic_amd64.deb

VOLUME ["/data"]

WORKDIR /data

# process cluster webui
EXPOSE 28015 29015 8080

CMD rethinkdb --bind all --config-file /etc/rethinkdb/default.conf
