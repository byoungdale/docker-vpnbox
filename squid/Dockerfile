# Build a docker image for squid proxy
FROM ubuntu:latest

WORKDIR /tmp

# Define which filters to use, check http://www.shallalist.de/categories.html for a list
ENV SQUIDGUARD_FILTER="adv spyware tracker"

# installing Squid from source because it's the only way to set the 
#  --enable-ssl-crtd --with-openssl
# flags for 'security_file_certgen' to be installed
RUN apt-get update && \
  apt-get install wget gcc gcc-c++ make perl curl openssl tar iproute iptables sudo && \
  cd /tmp/ && \
  wget http://www.squid-cache.org/Versions/v4/squid-4.4.tar.gz && \
  tar xvf squid-4.4.tar.gz && \
  cd squid-4.4 && \
  ./configure --enable-ssl-crtd --with-openssl && \
  make && \
  make install && \
  useradd squid && \
  cd /tmp/ && \
  apt-get install squidGuard && \
  rm -rf /tmp/* /var/tmp/* /var/log/*


ADD ./bin /usr/local/bin
ADD ./etc /etc/squid

# 3128 = standard explicit proxy (http)
# 3129 = TPROXY  (transparent proxy for http traffic)
# 3130 = TPROXY ssl_bump (transparent proxy for https traffic with bump)
EXPOSE 3128 3129 3130

# this script will create the CA used for ssl_bump, if not existing
ENTRYPOINT ["/usr/local/bin/run.sh"]
