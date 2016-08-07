FROM yoryan/insurgencyds
MAINTAINER Ryan Young <rayoung@utexas.edu>

COPY subscribed_file_ids.txt /srv/insurgency/insurgency_ds/insurgency/

# Download workshop items, stop server once it's starting a new game
RUN (/srv/insurgency/insurgency_ds/srcds_run -workshop >/tmp/srcds.log &) \
  && while ! grep '^---- Host_NewGame ----$' /tmp/srcds.log; do sleep 5; done \
  && pkill -2 srcds_run \
  && rm -f /tmp/srcds.log

COPY mapcycle_doi.txt /srv/insurgency/insurgency_ds/insurgency/
COPY server.cfg /srv/insurgency/insurgency_ds/insurgency/cfg/

ENTRYPOINT [ "/srv/insurgency/insurgency_ds/srcds_run", \
  "-workshop", \
  "+sv_pure", "0", \
  "-console", \
  "-port", "27015", \
  "-autoupdate", "-steam_dir", "/srv/insurgency/steamcmd", "-steamcmd_script", "/srv/insurgency/insurgency_ds.txt" ]
CMD [ "+map", "doi_bastogne_night", "+maxplayers", "32" ]

