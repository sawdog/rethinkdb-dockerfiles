from ubuntu:18.04
MAINTAINER Andrew Sawyers <andrew@sawdog.com>

RUN apt-get update \
    && apt-get install -y bash wget gnupg2

SHELL ["/bin/bash", "-c"]

# Add the rebirthDB repository and public key
# RebirthDB Packaging is currently borked; can't grab the deb from the -dev repo
#RUN source /etc/lsb-release \
# && echo "deb [trusted=yes] https://dl.bintray.com/rebirthdb-dev/apt $DISTRIB_CODENAME main" | tee /etc/apt/sources.list.d/rebirthdb.list \
# && echo "deb [trusted=yes] https://bintray.com/rebirthdb/apt/rebirthdb-dev/apt $DISTRIB_CODENAME main" | tee /etc/apt/sources.list.d/rebirthdb.list \
#    && wget -qO- https://dl.bintray.com/rebirthdb/keys/pubkey.gpg | apt-key add - \
#    && apt-get update \
#    && apt-get install -y rebirthdb

# temp workaround 
WORKDIR /tmp
COPY ./deb/rebirthdb_2.3.6+fallback~0bionic_amd64.deb ./
RUN apt install -y ./rebirthdb_2.3.6+fallback~0bionic_amd64.deb
RUN rm ./rebirthdb_2.3.6+fallback~0bionic_amd64.deb

VOLUME ["/data"]

WORKDIR /data

CMD ["rebirthdb", "--bind", "all"]

#   process cluster webui
EXPOSE 28015 29015 8080
