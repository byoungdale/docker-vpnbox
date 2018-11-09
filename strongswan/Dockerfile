# build docker image for strongswan
FROM ubuntu:18.04

WORKDIR /tmp

RUN apt-get update && \
  apt-get -y install software-properties-common lsb-release apt-utils build-essential

ADD ./bin /usr/local/bin

# this script will create the CA used for ssl_bump, if not existing
ENTRYPOINT ["/usr/local/bin/run.sh"]