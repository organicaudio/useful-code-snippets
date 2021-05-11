# my server setup

1. setup public infrastructure like vls, domain name and dns records 
2. setup server infrastructure like letsencrypt certificates, docker, kubernetes, nginx reverse proxy
3. setup applications like ci pipeline

## setup public infrastructure

1. get **virtual linux server** (vls) with public ip address 
2. reserve **domain name**
3. setup **dns record** to point domain name to vls ip


### concrete steps
- create cx11 vls in [hetzner cloud](https://www.hetzner.de/) 
- buy weyrich.dev domain at [namecheap](https://www.namecheap.com/) (14 €/year)
- [signup at cloudflare](https://dash.cloudflare.com/) and create a dns record. Cloudflare is used because it is free and it [supports multiple letsencrypt renewal clients](https://community.letsencrypt.org/t/dns-providers-who-easily-integrate-with-lets-encrypt-dns-validation/86438).
- set the two cloudflare dns server addresses to be used by namecheap [Here is a how-to](https://www.namecheap.com/support/knowledgebase/article.aspx/767/10/how-to-change-dns-for-a-domain)
- create A and AAAA entries in cloudflare which map the domain name to the vls ipv4 and ipv6 address
- (optional) create CNAME entry for every subdomain you want to use.

### cost
1. vls: 35.52 €/year
2. domain name: 14 €/year
3. dns record: free
4. wildcard certificate: free

### your dashboards
- [hetzner cloud console](https://console.hetzner.cloud/projects)
- [namecheap dashboard](https://ap.www.namecheap.com/)
- [cloudflare dashboard](https://dash.cloudflare.com/f)

## server infrastructure 

1. get **wildcard certificate** for domain and its subdomains with letsencrypt


## get letsencrypt wildcard certificate 

In order to use letsencrypt you need a acme compliant client. Certbot is the recommended one. So [setup certbot](https://certbot.eff.org/instructions) on your vls with **dns validation** (not http validation [see the differences](https://letsencrypt.org/de/docs/challenge-types/)) so you can create a **wildcard vertificate** for your domain.

You can either install the cerbot on you host system or you use docker to start it.

### setup certbot via install

```shell
# install certbot
sudo apt-get install certbot python-certbot-nginx

# install plugin for the dns provider cloudflare
sudo apt-get install python3-certbot-dns-cloudflare

# setup cloudflare credentials for certbot - https://certbot-dns-cloudflare.readthedocs.io/en/stable/

## create a api token in cloudflare dashboard with the:
### Zone:Zone:Read and Zone:DNS:Edit permissions for all zones

## save api your api key, mail address and api token in a file
touch ~/.certbot/cloudflare.ini
##add to the file:
#dns_cloudflare_email=<mail address>
#dns_cloudflare_api_key=<api key>
#dns_cloudflare_api_token=<created api token>


## acquire wildcard certificate for weyrich.dev, save the certs under /etc/letsencrypt/live/weyrich.dev/ and start a nginx on port
certbot \
  --dns-cloudflare \
  --dns-cloudflare-credentials ~/.certbot/cloudflare.ini \
  -i nginx \
  -d *.weyrich.dev

# test automatic renewal
sudo certbot renew --dry-run

# check your domain with ssllab: https://www.ssllabs.com/ssltest/
```

```shell
# reload config
sudo nginx -s reload

# renew certificate
certbot renew\
  --dns-cloudflare \
  --dns-cloudflare-credentials ~/.certbot/cloudflare.ini \
  -d *.weyrich.dev

# generate certificate
certbot certonly\
  --dns-cloudflare \
  --dns-cloudflare-credentials ~/.certbot/cloudflare.ini \
  -d *.weyrich.dev
```

### setup certbot via docker

[Blog entry](https://medium.com/faun/docker-letsencrypt-dns-validation-75ba8c08a0d) which explains hot wo setup a letsencrypt client with docker. The [linuxserver/letsencrypt](https://hub.docker.com/r/linuxserver/letsencrypt) docker image is used and configured to generate a wildcard certificate via dns validation. 

## setup docker

`curl -sSL https://get.docker.com | sh`

## setup nginx as reverse proxy

Base config is created with [this tool from digitalocean](https://www.digitalocean.com/community/tools/nginx). Afterwards for every subdomain a proxy_pass is configured. See the page **nginx memory aid** for an overview of nginx config. And remember to create a CNAME in the dns for every subdomain.

**The browser will heavily use caching when serving static files so remember to delete the caches after changing proxy settings.**