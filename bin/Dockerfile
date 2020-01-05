FROM debian:stretch

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl3-dev wget zip openssl procps

RUN apt-get install libcairo2-dev libnetpbm10-dev netpbm libpng-dev libjpeg-dev python-numpy python-pyfits python-dev zlib1g-dev libbz2-dev swig libcfitsio-dev -y --fix-missing


RUN cd /root && wget http://astrometry.net/downloads/astrometry.net-latest.tar.gz && tar xvzf astrometry.net-latest.tar.gz
RUN cd /root/astrometry.net-* && make && make py && make extra && make install
RUN cd /root && rm -r astro*

ENV PATH "$PATH:/usr/local/astrometry/bin"

RUN curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh && bash nodesource_setup.sh && apt install nodejs && rm nodesource_setup.sh

RUN cd /root && git clone https://github.com/thomome/astrometry-api-lite.git astrometry && cd astrometry && npm install && npm run all:build

WORKDIR /root/astrometry

CMD ["npm", "run", "server"]