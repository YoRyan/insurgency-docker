FROM ubuntu:16.04
MAINTAINER Ryan Young <rayoung@utexas.edu>

RUN apt-get update && apt-get -y install ca-certificates lib32gcc1 net-tools \
  && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get -y install wget \
  && groupadd -r insurgency && useradd -r -d /srv/insurgency -m -g insurgency insurgency \
  && mkdir -p /srv/insurgency/steamcmd \
  && wget -O - 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz' | tar xz -C /srv/insurgency/steamcmd \
  && chown -R insurgency:insurgency /srv/insurgency/steamcmd \
  && apt-get -y --purge remove wget \
  && apt-get -y --purge autoremove \
  && rm -rf /var/lib/apt/lists/*

COPY insurgency_ds.txt /srv/insurgency/

USER insurgency

RUN /srv/insurgency/steamcmd/steamcmd.sh +runscript /srv/insurgency/insurgency_ds.txt

EXPOSE 27015/udp 27015

ENTRYPOINT [ "/srv/insurgency/insurgency_ds/srcds_run", \
  "-console", \
  "-port", "27015", \
  "-autoupdate", "-steam_dir", "/srv/insurgency/steamcmd", "-steamcmd_script", "/srv/insurgency/insurgency_ds.txt" ]
CMD [ "+map", "market_coop", "+maxplayers", "32" ]

