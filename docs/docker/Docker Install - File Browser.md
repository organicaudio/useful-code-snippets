##  DOCKER - FILE BROWSER

**Quick Install Command*


```
curl -fsSL https://filebrowser.org/get.sh | bash filebrowser -r / -a 10.0.0.22 -
filebrowser -r /srv -a 10.0.0.22

curl -fsSL https://filebrowser.org/get.sh | bash
filebrowser -r / -a 10.0.0.99
```



## DOCKER INSTALL for UBUNTU 16.04



```
docker run \
    -v /:/srv \
    -v /opt/filebrowser/filebrowser.db:/database.db \
    -v /opt/filebrowser/.filebrowser.json:/.filebrowser.json \
    -p 5580:80 \
    filebrowser/filebrowser
```




## DOCKER INSTALL for RASPBERRY PI 3 (ARMv7)


```
docker run \
    -p 9980:80 \
    filebrowser/filebrowser
```




`docker pull filebrowser/filebrowser`



```
docker run \
    --name=filebrowser \
    -v /:/srv \
    -e PUID:1000 \
    -e GUID:1000 \
    -v /opt/filebrowser/filebrowser.db:/database.db \
    -v /opt/filebrowser/filebrowser.json:/.filebrowser.json \
    -p 80:80 \
    filebrowser/filebrowser
```



```
docker run --name=filebrowser2 -v /opt:/srv/opt -v /srv:/srv/srv -p 9980:80 filebrowser/filebrowser
```

