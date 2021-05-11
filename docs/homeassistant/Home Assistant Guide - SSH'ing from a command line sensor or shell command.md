# **Home Assistant Guide - SSH'ing from a command line sensor or shell command**

## What will this cover

This guide will walk through the process of getting a command which ssh’s into another machine to get some simple data ready to be included in a [command line sensor 7](https://www.home-assistant.io/integrations/sensor.command_line/). To keep it simple I’ll use the same example from the documentation (getting CPU temperature) I’ll just run it over SSH. The focus will more be on how to test correctly, how to set up the identity file and how to handle the known hosts file in a way that works with HA.

Note that these instructions could also easily apply to any of the [command line integrations 1](https://www.home-assistant.io/integrations#search/command%20line) or [shell command 8](https://www.home-assistant.io/integrations/shell_command/). Also these instructions are going to focus on users that installed HA via the [Home Assistant OS](https://www.home-assistant.io/hassio/installation/) and [Supervised](https://github.com/home-assistant/supervised-installer) install methods as this is where I’ve seen the most issues. It’s not useless in other install methods but it is going to talk about add-ons so those parts won’t be followable as is, you’ll have to adjust for your setup.

## Pre-Requisites

-   The [SSH & Web Terminal 4](https://github.com/hassio-addons/addon-ssh) from the list of community add-ons set up and with protection mode disabled (this is necessary to be able to execute commands on specific containers, more on this below)

**Portainer alternative**  
If you prefer to use the official [SSH & Terminal 3](https://github.com/home-assistant/addons/tree/master/ssh) addon or do not wish to disable protection mode on your SSH add-on then you can install the [Portainer add-on 5](https://github.com/hassio-addons/addon-portainer) add-on instead. You will still need to disable protection mode on the Portainer add-on (so we can see and run commands on other containers) but not on your SSH one in this case.

## Generating the id file

Since we’ll be running these commands from sensors or service calls, interactive SSH isn’t an option so we must go password-less (plus its a security best practice). So to start we need to generate an identity file. The easiest way to do this is just to `ssh` into HA (or open “Terminal” from the left side nav of your UI) and then follow [this guide 17](https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/) (or if you don’t like mine, search for “setting up password-less SSH” and pick the guide of your choice).

However there is one key exception, _do not store your key file in the default location_. The default location for `ssh-keygen` is `~/.ssh` which translates to `/root/.ssh`. You should not store anything in `/root` for a few reasons:

1.  It is not a shared folder between the docker containers. The SSH & Terminal add-on is actually a different docker container then the HA application which means they do not share a filesystem, they only share specific folders such as `/config` and `/share`. `/root` is not shared so anything you put in that folder while ssh’ed in like this is not visible to HA.
2.  Even if you do get to `/root` of the actual HA container, don’t use it. Only specific folders such as `/config` and `/share` are preserved across updates, everything else is wiped clean. So anything you do have stored in `/root` in the HA container will be lost next update.

Instead I’d recommend telling `ssh-keygen` to store its generated ID file in `/config/.ssh`. You don’t have to put it in a folder called `.ssh` if you don’t want to, I just like the consistency. But you should put it in `/config` so it is preserved over updates.

## Testing your command

Now that you have your ID file, lets test the command. To do this though, we can’t just run the command while SSH’ed in normally because _if your command works while ssh’ed into HA that does not mean it will work when run from HA via a command line sensor_.

The reason for this is because of the docker containers like I mentioned before. When you SSH into HA you’re actually ssh’ing into an add-on which is a different docker container from HA itself. Each docker container has its own filesystem and installed packages, successfully running it while ssh’ed really doesn’t tell you anything about whether it will work when run from HA.

This is where disabling protection mode comes in. While SSH’ed into HA execute the following command (thanks [@VDRainer](https://community.home-assistant.io/u/vdrainer)!):

`docker exec -it homeassistant bash` 

What this will do is open an interactive bash shell on the actual `homeassistant` container where HA runs. From this shell any commands we run will be run in exactly the same way HA will run them from a shell command or command line sensor. This way we know if they work from there then they will work from HA. So now we can run our command like so and confirm that it works:  

[![Screen Shot 2020-12-25 at 11.58.30 PM](https://community-assets.home-assistant.io/optimized/3X/f/5/f54167df78b37ecf012fb27aea64cb2e883e777c_2_690x127.png)](https://community-assets.home-assistant.io/original/3X/f/5/f54167df78b37ecf012fb27aea64cb2e883e777c.png "Screen Shot 2020-12-25 at 11.58.30 PM")

Note that for those unaware, `-i` is the flag to the `ssh` command which tells it where to find the identity file to use. Since we have put the identity file in an unusual location we must specify this. Sub in the name and location you used for yours.

Portainer alternative

For those using the official SSH add-on or without protection mode disabled on their SSH add-on you won’t be able to use `docker exec` like I suggested above. Instead open the Portainer add-on from the left side nav of HA. From there click on ‘containers’  
![Screen Shot 2020-12-22 at 10.38.27 AM](https://community-assets.home-assistant.io/original/3X/3/d/3d8c22959d58d424c5f0743bca2285e43cbae867.png)  
Then find the ‘homeassistant’ container in the list and click the little icon for ‘exec console’ like this:  

[![Screen Shot 2020-12-22 at 10.40.18 AM](https://community-assets.home-assistant.io/optimized/3X/1/2/1229bfb7b1fc0f8ee3c5fd67a9670168e3e6fee4_2_690x444.png)](https://community-assets.home-assistant.io/original/3X/1/2/1229bfb7b1fc0f8ee3c5fd67a9670168e3e6fee4.png "Screen Shot 2020-12-22 at 10.40.18 AM")

  
Then in this screen just click “connect” to launch a terminal window on this container as `root`:  
![Screen Shot 2020-12-22 at 10.42.39 AM](https://community-assets.home-assistant.io/original/3X/6/2/62f85474cec1a75da2576aad06a3dcbbe855ca1a.png)  
Now enter your command in the terminal that appears and run it like so:  

[![Screen Shot 2020-12-22 at 10.46.52 AM](https://community-assets.home-assistant.io/optimized/3X/9/2/92d3c73b6b0fa0aad7ac011abda0cdcdc209dc76_2_690x256.png)](https://community-assets.home-assistant.io/original/3X/9/2/92d3c73b6b0fa0aad7ac011abda0cdcdc209dc76.png "Screen Shot 2020-12-22 at 10.46.52 AM")

  
Running it this way runs it in exactly the same way that HA does so now I have confirmed my command is working and can be put in a command line sensor.

## Handling the `known_hosts` file

You’ll notice in my last screenshot that it asked me to verify the authenticity of the host. This is the final issue we have to tackle since we can’t have any interactive pieces in our final product.

Normally you just go through this once and then you are good to go, it never prompts you to verify authenticity again. However with HA this is another gotcha. The problem is that by default the `known_hosts` file is stored in `/root/.ssh`. Which means if you stop here your sensor will appear to work but will break next update when `/root` is wiped clean.

Fortunately, there’s a very simple solution to this, we just need to tell our command that the `known_hosts` file is somewhere that isn’t wiped clean every update. I would suggest also putting it within `/config/.ssh` but you can put it wherever you want, as long as its in somewhere like `/config` that is preserved over updates. Once you decide where to put it, add this to your command: `-o UserKnownHostsFile=/config/.ssh/known_hosts`. Then run your command once more from the `docker exec` shell with this addition (or from portainer if you are using the atlernative approach) so it updates your custom `known_hosts` file and then you are good to go:  

[![Screen Shot 2020-12-26 at 12.09.42 AM](https://community-assets.home-assistant.io/optimized/3X/a/6/a6f2f05679e28eb3e593733359fcb77c0b822d86_2_690x100.png)](https://community-assets.home-assistant.io/original/3X/a/6/a6f2f05679e28eb3e593733359fcb77c0b822d86.png "Screen Shot 2020-12-26 at 12.09.42 AM")

**Note:** I used `known_hosts_2` here because I already have a `known_hosts` file in this spot and I didn’t want to mess up my existing sensors by removing it. But again, you can call it whatever you want and put it wherever you want, as long as its somewhere in `/config`

**Alternative - no host key check**  
There is an alternative you will see around the forum here. If you add `-o StrictHostKeyChecking=no` to your command then it will turn off host verification entirely. This works as well and is probably fine if you are going between two systems on your local network. But since this is a security bad practice I’m recommending the other way. In the end the decision is up to you though.

## Command line sensor vs. Shell command

A few last things to be aware of. [Shell commands 8](https://www.home-assistant.io/integrations/shell_command/) runs in a restricted environment that doesn’t allow expanding the home director (`~`) or piping output of one command into another. This is the only situation I’ve personally run into so far where you have a command working in portainer that doesn’t work in HA. Make sure to read the documentation of the integrations you use to be aware of other integration specific gotchas like this.

Also if you are having trouble the command line integrations all log stdout and stderr if you set the [log level 5](https://www.home-assistant.io/integrations/logger/) of the integration you are trying to use to `debug`.

### Source:
https://community.home-assistant.io/t/sshing-from-a-command-line-sensor-or-shell-command/258731