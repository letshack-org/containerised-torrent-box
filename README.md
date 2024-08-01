# containerised-torrent-box

A collection of docker compose files to quickly spin up a torrent box.

```
git clone https://github.com/letshack-org/containerised-torrent-box.git
cd containerised-torrent-box
mv stacks /opt

```
# NOTE - Make sure to edit each compose.yml environment values to align with your personal setup.

Create the docker network the containers will use:

`docker network create torrent_net`

Then using a bash script like the below to bring the containers all up - 

```
#!/bin/bash

# Iterate through each folder in /opt/stacks
for stack_dir in /opt/stacks/*/; do
    if [ -d "$stack_dir" ]; then
        echo "Updating containers in $stack_dir"

        # Change directory to the stack directory
        cd "$stack_dir" || exit

        # Run docker-compose pull and docker-compose up -d
        docker compose pull && docker compose up -d

        # Change back to the original directory
        cd - || exit
    fi
done

```

Navigate to the Firefox container in your browser - https://ip-of-machine:3001

Then within the Firefox container we can access the rest of the containers. Bookmark the below:

qBittorrent Client - http://qbittorrent:8080/

File Browser - http://filebrowser:80/files

Sonarr - http://sonarr:8989/

Lidarr - http://lidarr:8686/

Radarr - http://radarr:7878/

Prowlarr - http://prowlarr:9696/


Note: Within Prowlarr we can use the flaresolverr proxy for any indexes that are using Cloudflare.

