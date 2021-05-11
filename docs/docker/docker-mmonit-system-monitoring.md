## DOCKER - MONIT & MMONIT

```
docker create \
  --name=monit \
  -e PUID=1000 \
  -e PGID=20 \
  -e TZ="America/New York" \
  -e MMONIT_LICENSE_OWNER="Current Health" \
  -e MMONIT_LICENSE_KEY="FAPYTFIOYG-AWQ5ZCQFLJ-TUBGQ4EBZK-5ZPXY62ADA-3F2TGRWZVN2XNXR6TQ6J-NRP3SAQC3A-YYUOGVMX35-HYI4I4ZO37-ZSROQ7ODNN    I3JERR7DF4-GYWG5LT46Z-CBWLDAND7T-BOR736U2UD-XZURINBYDDZO6VFVZ5WL-AZTZBQ2A7R-ZHMI2SWMZJ-27JT5P772I-EPIH6TAAP3CCBFU" \
  --expose 5588 \
  -v /opt/mmonit:/config \
  --restart unless-stopped \
  jchonig/mmonit

```

**Mmonit License Key (VALID())**
```
<License owner="Current Health">
    FAPYTFIOYG-AWQ5ZCQFLJ-TUBGQ4EBZK-5ZPXY62ADA-3F2TGRWZVN
    2XNXR6TQ6J-NRP3SAQC3A-YYUOGVMX35-HYI4I4ZO37-ZSROQ7ODNN
    I3JERR7DF4-GYWG5LT46Z-CBWLDAND7T-BOR736U2UD-XZURINBYDD
    ZO6VFVZ5WL-AZTZBQ2A7R-ZHMI2SWMZJ-27JT5P772I-EPIH6TAAP3
    CCBFU
</License>
```

**Docker Install Monit:**
```
docker create \
  --name=monit \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -e MMONIT_LICENSE_OWNER="Fred" \
  -e MMONIT_LICENSE_KEY="<M/Monit license key>" \
  --expose 8080 \
  -v /opt/mmonit/:/config \
  --restart unless-stopped \
  jchonig/mmonit
```