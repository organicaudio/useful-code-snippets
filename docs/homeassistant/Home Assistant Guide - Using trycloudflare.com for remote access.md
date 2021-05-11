---
created: 2021-05-11T02:45:13 (UTC -04:00)
tags: []
source: https://community.home-assistant.io/t/using-trycloudflare-com-for-remote-access-to-home-assistant/298184
author: 
---

# Home Assistant Guide - Using trycloudflare.com for remote access

> ## Excerpt
> The Problem At the moment, configuration for remotely accessing your home assistant installation requires that you either pay for Home Assistant Cloud or perform a rather complex setup to get a domain name, a SSL certificate, and forward ports from your home router to your home assistant installation.  Some of you might be unable to forward ports, or don’t want to mess with the complexities of things like duckdns and letencrypt for certs.  This guide is designed to describe how you can use a fr...

---
At the moment, configuration for remotely accessing your home assistant installation requires that you either pay for Home Assistant Cloud or perform a rather complex setup to get a domain name, a SSL certificate, and forward ports from your home router to your home assistant installation.

Some of you might be unable to forward ports, or don’t want to mess with the complexities of things like duckdns and letencrypt for certs.

This guide is designed to describe how you can use a free service offered by cloudflare to get your home assistant installation online.

It is a completely free service (doesn’t even require an account) that allows you to create a tunnel from a service (in our case Home Assistant) running on your home network to a randomly generated domain name provided by Cloudflare. The service is completely free to use, but it does not have guaranteed uptime and is often used to test new features. However, in my testing it has been rock solid and I’ve had zero issues.

Feel free to checkout the Cloudflare blog post for more info on how it works: [A free Argo Tunnel for your next project 8](https://blog.cloudflare.com/a-free-argo-tunnel-for-your-next-project/)

The major advantage is that you do not need to open ports on your firewall or have a public IP address from your ISP. This allows your to with a single command get remote access to your home assistant installation regardless of how you get internet.

Each time the add-on starts you will get a new URL from Cloudflare, at the moment this is unavoidable, so please be aware that you may need to update the URL you use each time the add-on restarts.

[Addons for Home Assistant by Keaton 11](https://github.com/keatontaylor/addons)

I’ve created an add-on which you can add to Home Assistant OS at the link above. You’ll need to install it (for now installation make take a while as it does local builds).

Once installed configure the url in to point to your local http url for home assistant, for example: [http://192.168.1.54:8123](http://192.168.1.54:8123/)

After starting the add-on go to the logs and you should see a URL for [try.cloudflare.com 21](http://try.cloudflare.com/). That will be your new external URL to use to access home assistant.

This is entirely dependent on your installation method, but regardless of your how you have Home Assistant installed you’ll need to download the cloudflared binary.

1.  Download the latest [cloudflared binary 4](https://github.com/cloudflare/cloudflared/releases/) for your system. (You can even run it on your computer)
2.  Once downloaded you’ll need to open your command line or terminal on your computer.
3.  You’ll navigate to the folder from your download of cloudflared.
4.  Run the command `./cloudflared tunnel --url http://<home assistant local ip>:8123`
5.  Wait for the cloudflared app to give you a domain name.
6.  Access your home assistant installation by going to that URL.

Note: you’ll need to keep the cloudflared app running in the background to keep things operational.

I’d love to get some community support on this. I feel like it would be awesome to get an add-on created for Home Assistant OS users. They could have a one click installation for their devices and get a publicly accessible domain name for Home Assistant.

Since home assistant using this method will be running and backed by Cloudflare there are some protections they provide out of the box that will already be better than just raw port forwarding. However, is is strongly recommended to enable IP banning in your home assistant installation for failed login attempts to ensure things are kept secure, see: [HTTP - Home Assistant 2](https://www.home-assistant.io/integrations/http/) for more info on how to setup a login attempt threshold and enable IP banning.
