FROM ubuntu:15.04

# Install packages
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y install \
wget \
curl \
gdebi \
php5 \
sudo \
apache2\
apt-utils

RUN echo '#!/bin/sh' > /usr/sbin/policy-rc.d \
    && echo 'exit 101' >> /usr/sbin/policy-rc.d \
    && chmod +x /usr/sbin/policy-rc.d

RUN wget http://downloads.sourceforge.net/project/capanalysis/version%201.2.0/capanalysis_1.2.0_amd64.deb

RUN apt-get update && gdebi --n capanalysis_1.2.0_amd64.deb

RUN sed -i -e 's/PRIORITY=1 #(0..20)/PRIORITY=0 #(0..20)Z/g' /etc/init.d/capanalysis

CMD sudo service postgresql restart && \
sudo service apache2 restart && \
sudo service capanalysis restart && \
tail -f /var/log/apache2/access.log