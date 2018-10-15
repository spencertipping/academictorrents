FROM ubuntu:18.04
RUN apt-get update \
 && apt-get -y install \
      curl wget less \
      xzip p7zip-full unzip pbzip2 \
      perl libsys-mmap-perl bittorrent

ADD ni /usr/bin/

VOLUME /data
VOLUME /tmp

CMD /bin/bash
