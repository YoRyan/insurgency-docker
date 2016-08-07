# insurgency-docker
Docker images for Insurgency and its Day of Infamy beta mod.

The insurgencyds image is built with the latest Insurgency dedicated server
from steamcmd. The dayofinfamyds image adds the Day of Infamy total
conversion workshop items per [the instructions on the /r/insurgency
wiki](https://www.reddit.com/r/insurgency/wiki/server_linux_doi).

An auto-update script is included in the build.

# usage

You need to at least open 27015/udp to play.

    docker run -d -p 27015:27015/udp yoryan/insurgencyds

You can add a custom server.cfg and map playlists using host mounts. The path to
the server's cfg directory is `/srv/insurgency/insurgency_ds/insurgency/cfg/`.

    docker run -d -p 27015:27015/udp -v /path/to/my/server.cfg:/srv/insurgency/insurgency_ds/insurgency/cfg/server.cfg yoryan/insurgencyds

To control the server, you can use rcon or use `docker run -it` or
`docker attach` to gain control of the console.
