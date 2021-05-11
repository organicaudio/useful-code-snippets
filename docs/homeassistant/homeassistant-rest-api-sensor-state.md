## PHILIPS HUE LABS - DISABLE  MOTION SENSOR SCRIPT

**WHAT:**
HTTP Post commands that remotely trigger a change in state to a sensor on HASSIO

```
curl -X POST -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNjQ4OTA1M2YxOTU0YWY5ODgwMjAyMTIyNmYzYjQ0ZSIsImlhdCI6MTYxMDk3MjMwNiwiZXhwIjoxOTI2MzMyMzA2fQ.Quwnk-2wElJcMcn5J-SJUCKvpA2i000BgUGQJtS-sz8" \
  -H "Content-Type: application/json" \
  -d '{"state": "awake", "attributes": {"friendly_name": "Macbook - Status"}}' \
  http://10.0.0.99:8123/api/states/sensor.macbook_status
```

```
  curl -X POST -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNjQ4OTA1M2YxOTU0YWY5ODgwMjAyMTIyNmYzYjQ0ZSIsImlhdCI6MTYxMDk3MjMwNiwiZXhwIjoxOTI2MzMyMzA2fQ.Quwnk-2wElJcMcn5J-SJUCKvpA2i000BgUGQJtS-sz8" -H "Content-Type: application/json" -d '{"state": "sleep", "attributes": {"friendly_name": "Macbook - Status"}}' http://10.0.0.99:8123/api/states/sensor.macbook_status

```

```
  /usr/bin/curl -X POST -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNjQ4OTA1M2YxOTU0YWY5ODgwMjAyMTIyNmYzYjQ0ZSIsImlhdCI6MTYxMDk3MjMwNiwiZXhwIjoxOTI2MzMyMzA2fQ.Quwnk-2wElJcMcn5J-SJUCKvpA2i000BgUGQJtS-sz8" -H "Content-Type: application/json" -d '{"state": "awake", "attributes": {"friendly_name": "Macbook - Status"}}' http://10.0.0.99:8123/api/states/sensor.macbook_status    
```


