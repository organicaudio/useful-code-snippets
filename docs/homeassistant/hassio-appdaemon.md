## DOCKER - HASSIO - APPDAEMON



```
docker run --name=appdaemon -d -p 5050:5050 \
  --restart=always \
  -e HA_URL="http://10.0.0.99:8123" \
  -e TOKEN="gffTn4IGJkHJtvNm36ZZeJmkNzyVdVpeg7WxDkXJpHg" \
  -e DASH_URL="http://$HOSTNAME:5050" \
  -v /opt/hassio/appdaemon:/conf \
  appdaemon:latest
```
