# nginx memory aid


Nice tool to [generate a nginx config](https://www.digitalocean.com/community/tools/nginx). You may need to generate a Diffie-Hellman parameter for DHE ciphersuites: `openssl dhparam -out dhparam.pem 4096`

[Guide how to configure nginx as reverse proxy with tls and docker](https://medium.com/free-code-camp/docker-nginx-letsencrypt-easy-secure-reverse-proxy-40165ba3aee2)

## directories

- config: /etc/nginx
- logs: /var/log/nginx
- files which getting served: /var/www

## commands

- `nginx` - start server
- `nginx -s stop` - stop the server
- `nginx -s reload` - reload the config
- `nginx -t` - test config
- `ln -s /etc/nginx/sites-available/weyrich.dev.conf /etc/nginx/sites-enabled/weyrich.dev.conf` - create symlink from a conf file in sites-available to sites-enabled. **Remember to use a full qualified path**

## configuration

- global config /etc/nginx/nginx.conf set some standard settings and loads the config files in following two folders.
- Files in /etc/nginx/conf.d/ which ends with .conf
- Files in /etc/nginx/sites-enabled which are usually only a symlink to files in /etc/nginx/sites-available. Contains the *default* configuration of nginx.

## configuration directives

[Reference](http://nginx.org/en/docs/http/ngx_http_core_module.html)


The [guide](https://www.digitalocean.com/community/tutorials/understanding-nginx-server-and-location-block-selection-algorithms) on how config blocks are chosen by nginx is nice. The outline is:

1. find server block with the most 'specific' ip address and port in the **listen** directive 
2. if multiple listen directives are equally specific (or just equal) then the **server_name** directive will decide which will execute it. Search for the most 'specific one'
   

Example of reverse proxy with tls support which proxies to a non-tls server (except for the subdomain it is generated the [tool](https://www.digitalocean.com/community/tools/nginx)):

```nginx
server {
	listen 78.47.255.193:443 ssl http2;
	listen [::]:443 ssl http2;

	server_name weyrich.dev;
	root /var/www/weyrich.dev/public;

	# SSL
	ssl_certificate /etc/letsencrypt/live/weyrich.dev/fullchain.pem;
	ssl_certificate_key /etc/letsencrypt/live/weyrich.dev/privkey.pem;

	# security
	include nginxconfig.io/security.conf;

	# logging
	access_log /var/log/nginx/weyrich.dev.access.log;
	error_log /var/log/nginx/weyrich.dev.error.log warn;

	# index.html fallback
	location / {
		try_files $uri $uri/ /index.html;
	}

	# additional config
	include nginxconfig.io/general.conf;
}

# ci subdomains proxy pass
server {
	listen 78.47.255.193:443 ssl http2;
	listen [::]:443 ssl http2;

	server_name ci.weyrich.dev;

	# security
	include nginxconfig.io/security.conf;

	# logging
	access_log /var/log/nginx/ci.weyrich.dev.access.log;
	error_log /var/log/nginx/ci.weyrich.dev.error.log warn;

	# reverse proxy
	location / {
		proxy_pass http://127.0.0.1:180/;
		include nginxconfig.io/proxy.conf;
	}
}

# HTTP redirect
server {
	listen 78.47.255.193:80;
	listen [::]:80;

	server_name .weyrich.dev;

	return 301 https://weyrich.dev$request_uri;
}


```