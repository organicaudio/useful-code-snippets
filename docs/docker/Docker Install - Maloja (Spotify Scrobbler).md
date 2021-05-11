## DOCKER - MALOJA (Spotify Scrobble)

**Repo:**
[https://github.com/krateng/maloja#docker](https://github.com/krateng/maloja#docker)

`docker pull joniator/maloja`

**Install:**
```
docker run -e "27ee50e60dc44eb1916bef44c42ba6fa=yourId" -e "b910ce2eecf0432d8b7bfc30034621c0=yourSecret" -e "MALOJA_URL=" -e "MALOJA_API_KEY=1234" -v /path/on/host/config:/home/node/app/config foxxmd/spotify-scrobbler
```
```
docker run --name=maloja-scrobble-server -d -p 9080:80 -e PUID=1000 -e PGID=1000 -e TZ=America/Toronto -e MALOJA_DATA_DIRECTORY=/opt/maloja -e MALOJA_SKIP_SETUP=true -e MALOJA_FORCE_PASSWORD=whydoyouwantit joniator/maloja
```
```
docker run --name=maloja-scrobble-server -d -p 5587:80 -e PUID=1000 -e PGID=1000 -e TZ=America/Toronto -e MALOJA_DATA_DIRECTORY=/opt/maloja -e MALOJA_SKIP_SETUP=true -e MALOJA_FORCE_PASSWORD=whydoyouwantit joniator/maloja 
```

