# build docker image for strongswan
FROM ubuntu:latest

WORKDIR /tmp

# this script will create the CA used for ssl_bump, if not existing
ENTRYPOINT ["/usr/local/bin/run.sh"]