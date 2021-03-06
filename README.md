[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[cardurl]: https://github.com/cardigann/cardigann
[hub]: https://hub.docker.com/r/lsioarmhf/cardigann/

THIS IMAGE IS DEPRECATED. PLEASE USE THE MULTI-ARCH IMAGES AT `linuxserver/cardigann`

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/cardigann
[![](https://images.microbadger.com/badges/version/lsioarmhf/cardigann.svg)](https://microbadger.com/images/lsioarmhf/cardigann "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/cardigann.svg)](https://microbadger.com/images/lsioarmhf/cardigann "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/cardigann.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/cardigann.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/armhf/armhf-cardigann)](https://ci.linuxserver.io/job/Docker-Builders/job/armhf/job/armhf-cardigann/)

[Cardigann][cardurl], a server for adding extra indexers to Sonarr, SickRage and CouchPotato via Torznab and TorrentPotato proxies. Behind the scenes Cardigann logs in and runs searches and then transforms the results into a compatible format. 

[![cardigan](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/cardigan.png)][cardurl]

## Usage

```
docker create \
  --name=cardigann \
  -v <path to data>:/config \
  -e PGID=<gid> -e PUID=<uid>  \
  -p 5060:5060 \
  lsioarmhf/cardigann

```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 5060` - the port(s)
* `-v /config` - Where cardigann should store it's config files
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e SOCKS_PROXY` - for using a socks proxy - *optional*
* `-e HTTP_PROXY` - for using an HTTP proxy - *optional*

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it cardigann /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

Configure via the webui at `<your-ip>:5060`

By adding a variable to the run command, `SOCKS_PROXY` or `HTTP_PROXY` cardigann can be used with a proxy, *eg* `-e SOCKS_PROXY=localhost:1080`

The folder /config/definitions can be used to add additional tracker definitions (for more info see [Additional definitions](https://github.com/cardigann/cardigann#definitions)

## Info

* Shell access whilst the container is running: `docker exec -it cardigann /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f cardigann`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' cardigann`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/cardigann`

## Versions

+ **22.08.18:** Rebase to alpine 3.8.
+ **06.05.18:** Use buildstage in Dockerfile.
+ **19.12.17:** Rebase to alpine 3.7.
+ **12.08.17:** Add npm install to build stage.
+ **29.05.17:** Rebase to alpine 3.6.
+ **09.02.17:** Rebase to alpine 3.5.
+ **03.11.16:** Compiled using [sstamoulis's](https://github.com/sstamoulis) method.
+ **01.11.16:** Initial Release.
