# Minidlna docker image

## Setup

Minidlna is configured to use **inotify** watches. Ensure you have enough on your Docker host with:

```bash
$ echo 'fs.inotify.max_user_watches = 200000' | sudo tee /etc/sysctl.d/99-inotify-max_user_watches.conf
$ sudo sysctl -p --system
```

## Tags

* *latest*: for **x86_64** hosts.
* *arm32v7*: for **Raspberry Pi 2 / 3** hosts.

## Run

```bash
$ docker run \
    -d \
    --name minidlna \

    # Needed for inotify
    -v /etc/localtime:/etc/localtime:ro \

    # Add as many of media folder needed. Example:
    #   -v /path/to/movies:/media/movies
    #   -v /path/to/series:/media/series
    -v <path_to_media_folder>:/media \

    # Optional: load a custom minidlna configuration file.
    -v <path_to_config_file>:/etc/minidlna.conf:ro \

    # Network settings
    --network host \
    -p 1900:1900/udp \
    -p 8200:8200/tcp \

    # Image to use
    bigbrozer/minidlna:latest
```
