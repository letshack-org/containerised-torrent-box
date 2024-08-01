# containerised-torrent-box

A collection of docker compose files to quickly spin up a torrent box.

```
cd /opt/
git clone https://github.com/letshack-org/containerised-torrent-box.git
```
Then using a bash script like below to bring them all up

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
