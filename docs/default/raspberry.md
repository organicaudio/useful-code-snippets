# raspberry pi

## installation

- use [Etcher](https://www.balena.io/etcher/) to create the image
- add a ssh file to the root of the boot partition to activate ssh like explained [here](https://hackernoon.com/raspberry-pi-headless-install-462ccabd75d0)
- start raspberry pi (and connect to lan wire so you can start right away from the remote computer)
- use ssh to connect to rp
- use `sudo raspi-config` to configure the rp
- (optional) install pip: `sudo apt-get install python-pip`

## power off and restart

```
# shutdown alias
sudo poweroff

# restart alias
sudo reboot

# shutdown
sudo shutdown -h now

# restart
sudo shutdown -r now
```

## install pip

```shell
sudo apt-get update
sudo apt-get install python-pip
```

## install docker on rp

```shell
# install
curl -sSL https://get.docker.com | sh


# add use pi to docker group
sudo usermod -aG docker pi

# reboot
sudo reboot

# test setup
docker run hello-world

# hello-world might not work. In this case than use (https://stackoverflow.com/questions/52233182/docker-run-does-not-display-any-output)
docker run hypriot/armhf-hello-world
```

## docker images for rp

In order to run on a rp a docker image need to be compiled for arm processor architecture. You can find a list of supported cpu architectures for docker [here](https://github.com/docker-library/official-images#architectures-other-than-amd64). To find out which architecture your rp has [see](https://de.wikipedia.org/wiki/Raspberry_Pi#Hardware). E.g. a rp 2 mod B uses a ARMv7 architecture.

- [open-jdk](https://hub.docker.com/r/balenalib/raspberry-pi-openjdk)

## install ranchers k3s kubernetes on rp

**the cpu of the rp 2 mod B seems to be to weak to run k3s server. Always on 100% and timeout on kubectl commands**

[Guide](https://opensource.com/article/20/3/kubernetes-raspberry-pi-k3s)

```shell
# install k3s on rp and start server ('systemd: Starting k3s' will take a looong time)
curl -sfL https://get.k3s.io | sh -

# after startup test if it runs
sudo kubectl get nodes
```

[Uninstall](https://rancher.com/docs/k3s/latest/en/installation/uninstall/):

- server node: `/usr/local/bin/k3s-uninstall.sh`
- agent node: `/usr/local/bin/k3s-agent-uninstall.sh`

## why i ditch my rp over a vls

- i want a **public ip** e.g. to use GitHub webhooks
  - via router can be tricky
  - via ngrok you do not get a static url
- many docker container wont run on **arm**
- my rp (2b+) is **to weak** to run k3s kubernetes 
- 