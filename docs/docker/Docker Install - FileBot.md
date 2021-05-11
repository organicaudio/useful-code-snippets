## Docker Install - FileBot

**What:**
FileBot is the ultimate tool for organizing and renaming your Movies, TV Shows and Anime as well as fetching subtitles and artwork. It's smart and just works.

**Links:**
[https://www.filebot.net](https://www.filebot.net)
[https://github.com/filebot/filebot-docker](https://github.com/filebot/filebot-docker)

**CLI:**


```
docker run --rm -it -v $PWD:/volume1 -v data:/data -p 5452:5452 -e FILEBOT_NODE_AUTH=BASIC -e FILEBOT_NODE_AUTH_USER=SECRETNAME -e FILEBOT_NODE_AUTH_PASS=SECRETPASS -p 5453:5453 -v /etc/ssl:/etc/ssl:ro -e FILEBOT_NODE_HTTPS=NO -e FILEBOT_NODE_HTTPS_PORT=5453 -e FILEBOT_NODE_HTTPS_KEY=/etc/ssl/private/server.key -e FILEBOT_NODE_HTTPS_CRT=/etc/ssl/certs/server.crt rednoah/filebot:node
```



