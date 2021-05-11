![apk-command](https://www.cyberciti.biz/media/new/faq/2017/05/apk.png)

I am new Alpine Linux system admin user. How do I use apk command line utility for the package management on Apline Linux server running in cloud or a Linux container? How can I use the apk command for the package management?  
  

Alpine Linux is a free and open source Linux-based distro. It uses musl and busybox. It is designed with security in mind and targeted at power users who wants secure distro out of the box. It uses PaX and grsecurity for Linux kernel protection. All binaries are compiled with stack smashing protection. APK stands for Alpine Linux package manager. You use the apk command to delete, install, upgrade, or list software on a running Alpine Linux based system. Like most modern Linux distro all software packages for Alpine Linux are digitally signed to avoid security problems. You can install packages from local disk (such as CDROM or a USB stick) or the internet archive location (repositories) such as http://dl-cdn.alpinelinux.org/alpine/v3.5/main. The list of repositories is stored in /etc/apk/repositories configuration file. 


Use the [cat command] to view /etc/apk/repositories file i.e. type cat /etc/apk/repositories. Alpine Linux package often has the .apk extension and called as “a-packs”. The apk command is equivalent to [apt command] / [apt-get command]  on Debian/Ubuntu on [yum command] on CentOS Linux.

## Purpose

> Use apk for installing, upgrading, configuring, and removing apps/programs for an Alpine Linux operating system in a consistent manner.

## Syntax

The basic syntax is as follows:

apk \[options\] command  
apk \[options\] command pkgName  
apk \[options\] command pkgName1 pkgName2

## Alpine Linux apk command examples

Let us see how to use the apk command to install security updates or new set of packages on an Alpine Linux server.

## How to update the package list

To update your package list, enter:  
`# apk update`  
Sample outputs:  

![Fig.01: How to update the package list in Alpine Linux](https://www.cyberciti.biz/media/new/faq/2017/05/apk-update-the-package.jpg)

Fig.01: How to update the package list in Alpine Linux

## How to search for package(s)

The syntax is:  
`# apk search pkgName`  
For example, search a package named htop, run:  
`# apk search htop`  
Sample outputs:

htop-doc-2.0.2-r0
htop-2.0.2-r0

To search and display description:  
`# apk search -v -d 'htop'`  
Sample outputs:

htop-doc-2.0.2-r0 - An interactive process viewer (documentation)
htop-2.0.2-r0 - An interactive process viewer

### To list all packages available, along with their descriptions

`# apk search -v`  
Sample outputs:

gettext-0.19.8.1-r0 - GNU locale utilities
gst-plugins-base0.10-dev-0.10.36-r3 - GStreamer Multimedia Framework Base Plugins (development files)
xcb-util-keysyms-dev-0.4.0-r0 - Utility libraries for XC Binding - keysyms (development files)
openlibm-0.5.4-r0 - High quality system independent, portable, open source libm implementation
imapsync-doc-1.727-r1 - IMAP synchronisation, sync, copy or migration tool (documentation)
evince-lang-3.22.1-r0 - Languages for package evince
jack-1.9.10-r2 - The Jack Audio Connection Kit
php7-intl-7.0.16-r0 - PHP7 extension: intl
php5-5.6.30-r0 - The PHP language runtime engine
samba-libs-4.5.7-r0 - Samba core libraries
gst-plugins-bad1-1.8.3-r0 - GStreamer bad plugins
docker-bash-completion-1.12.6-r0 - Bash completion for Docker
mesa-gl-12.0.3-r0 - Mesa libGL runtime libraries
nagios-plugins-mrtg-2.1.4-r2 - Nagios plugin check\_mrtg
.....
..
....
nrpe-2.15-r4 - NRPE allows you to remotely execute Nagios plugins on other Linux/Unix machines.
py2-psycopg2-2.6.2-r1 - A Python-PostgreSQL Database Adapter (for python2)
perl-mime-types-2.13-r0 - Definition of MIME types
perl-net-http-doc-6.09-r0 - Net::HTTP perl module (documentation)
shared-mime-info-lang-1.8-r0 - Languages for package shared-mime-info
altermime-0.3.11-r0 - alterMIME - MIME encoded email pack alteration tool
at-3.1.20-r0 - AT and batch delayed command scheduling utility and daemon
fbida-2.12-r0 - Few applications to display and elementary edit images

### How do I search package by wildcards?

The syntax is as follows to search all php7 packages or php5 packages:  
`# apk search -v 'php5*'  
### OR ###  
# apk search -v 'php7*'`  
Sample outputs:

php7-intl-7.0.16-r0 - PHP7 extension: intl
php7-openssl-7.0.16-r0 - PHP7 extension: openssl
php7-dba-7.0.16-r0 - PHP7 extension: dba
php7-sqlite3-7.0.16-r0 - PHP7 extension: sqlite3
php7-pear-7.0.16-r0 - PHP Extension and Application Repository
php7-phpdbg-7.0.16-r0 - Interactive PHP debugger
php7-litespeed-7.0.16-r0 - PHP LiteSpeed SAPI
php7-gmp-7.0.16-r0 - PHP7 extension: gmp
php7-pdo\_mysql-7.0.16-r0 - PHP7 extension: pdo\_mysql
php7-pcntl-7.0.16-r0 - PHP7 extension: pcntl
php7-common-7.0.16-r0 - The PHP language runtime engine - 7th branch (common config)
php7-xsl-7.0.16-r0 - PHP7 extension: xsl
php7-fpm-7.0.16-r0 - PHP FastCGI Process Manager
php7-mysqlnd-7.0.16-r0 - PHP7 extension: mysqlnd
php7-enchant-7.0.16-r0 - PHP7 extension: enchant
php7-pspell-7.0.16-r0 - PHP7 extension: pspell
php7-snmp-7.0.16-r0 - PHP7 extension: snmp
....
..
...
php7-sockets-7.0.16-r0 - PHP7 extension: sockets
php7-soap-7.0.16-r0 - PHP7 extension: soap
php7-apcu-5.1.8-r0 - PHP extension APC User Cache
php7-sysvmsg-7.0.16-r0 - PHP7 extension: sysvmsg
php7-zlib-7.0.16-r0 - PHP7 extension: zlib
php7-ftp-7.0.16-r0 - PHP7 extension: ftp
php7-sysvsem-7.0.16-r0 - PHP7 extension: sysvsem
php7-pdo-7.0.16-r0 - PHP7 extension: pdo
php7-bz2-7.0.16-r0 - PHP7 extension: bz2
php7-mysqli-7.0.16-r0 - PHP7 extension: mysqli

## How to install a package(s) by name

The syntax is:  
`# apk add pkgName  
# apk add pkgName1 pkgName2`  
To install a htop package, run:  
`# apk add htop`  
Sample outputs:

(1/1) Installing htop (2.0.2-r0)
Executing busybox-1.25.1-r0.trigger
OK: 39 MiB in 28 packages

To install Apache2 along with PHP7 and modules, run:  
`# apk add apache2 php7-apache2 php7-gd php7-mysqli`  
Sample outputs:

(1/28) Installing libuuid (2.28.2-r1)
(2/28) Installing apr (1.5.2-r1)
(3/28) Installing expat (2.2.0-r0)
(4/28) Installing apr-util (1.5.4-r2)
(5/28) Installing pcre (8.39-r0)
(6/28) Installing apache2 (2.4.25-r0)
Executing apache2-2.4.25-r0.pre-install
(7/28) Installing php7-common (7.0.16-r0)
(8/28) Installing libedit (20150325.3.1-r3)
(9/28) Installing libxml2 (2.9.4-r2)
(10/28) Installing php7-apache2 (7.0.16-r0)
(11/28) Installing libxau (1.0.8-r1)
(12/28) Installing libxdmcp (1.1.2-r2)
(13/28) Installing libxcb (1.12-r0)
(14/28) Installing libx11 (1.6.4-r0)
(15/28) Installing libxext (1.3.3-r1)
(16/28) Installing libice (1.0.9-r1)
(17/28) Installing libsm (1.2.2-r0)
(18/28) Installing libxt (1.1.5-r0)
(19/28) Installing libxpm (3.5.12-r0)
(20/28) Installing libbz2 (1.0.6-r5)
(21/28) Installing libpng (1.6.25-r0)
(22/28) Installing freetype (2.7-r1)
(23/28) Installing libjpeg-turbo (1.5.1-r0)
(24/28) Installing libwebp (0.5.2-r0)
(25/28) Installing php7-gd (7.0.16-r0)
(26/28) Installing mariadb-common (10.1.22-r0)
(27/28) Installing mariadb-client-libs (10.1.22-r0)
(28/28) Installing php7-mysqli (7.0.16-r0)
Executing busybox-1.25.1-r0.trigger
OK: 64 MiB in 56 packages 

### Interactive install or upgrade

We can force confirmation before performing certain operations by passing the \-i option:  
`# apk -i add nginx  
# apk -i upgrade`

The following packages will be upgraded:
  libcrypto1.1 libssl1.1 alpine-base linux-lts xtables-addons-lts openssh-keygen openssh-client openssh-sftp-server openssh-server-common openssh-server openssh openssl zfs-lts
After this operation, 16 KiB of additional disk space will be used.
Do you want to continue \[Y/n\]?

### Simulation with apk command

We can simulate the requested operation without making any changes. Helpful to see what packages will be upgrades or what will be done on the Alpine Linux system:  
`# apk -s command  
# apk -s add nginx  
# apk -s upgrade`  
In other words, nothing was installed or upgraded on the system, but you will know precisely what apk was about to do.

### How to hold a specific package back and not upgrade it

If you want to upgrade Alpine Linux system, but keep or hold a specific package add version number. For instance, to hold the bash package to the version 5.0.0-r0 level or lower, run:  
`# apk add bash**=**5.0.0-r0`  
One can do regex based version matching to hold the version to a major/minor release. For example:  
`# apk add bash**=~**5.0`  
Now, upgrade the system. However, apk will upgrade the entire system, keeping the bash package at the 5.0.0-r0 or lower level:  
`# apk upgrade`  
It is possible to remove holding. For example, make sure upgrade bash to the current lastest version, run:  
`# apk add bash**>**5.0.0-r0`  
![Alpine Linux apk Command Examples](https://www.cyberciti.biz/media/new/faq/2017/05/Alpine-Linux-apk-Command-Examples.png)

### How do install a local .apk file package?

The syntax is as follows to add a local package named foo.apk:  
`# apk add --allow-untrusted /path/to/foo.apk  
apk add --allow-untrusted pkg1.apk pkg2.apk`

## How to remove or delete a package(s) by name

The syntax is:  
`# apk del pkgName  
# apk del pkgName1 pkgName2`  
To delete a htop package run:  
`# apk del htop`  
Sample outputs:

(1/1) Purging htop (2.0.2-r0)
Executing busybox-1.25.1-r0.trigger
OK: 39 MiB in 27 packages

### How do I delete old packages caches on Alpine Linux?

To remove out older versions of packages, run the clean command as follows:  
`# apk cache clean  
## or ##  
# apk -v cache clean`  
One can also clean cache and download missing packages in one step:  
`# apk cache -v sync`

## How to upgrade running Alpine Linux

The syntax is:  
`# apk update && apk upgrade`  
You [can create a bash shell alias as follows](https://www.cyberciti.biz/tips/bash-aliases-mac-centos-linux-unix.html) in [~/.bashrc](https://bash.cyberciti.biz/guide/~/.bashrc)  
`# echo "alias update='apk update && apk upgrade'" >> /.bashrc`  
Run it as follows:  
`# update`

### How do I upgrade selected packages only?

The syntax is  
`# apk add -u pkgName`  
To upgrade a htop only package:  
`# apk update  
# apk add -u htop`

## How do I list installed packages?

The syntax is:  
`# apk info  
# apk info -vv | grep 'foo'  
# apk info -vv | sort`  

![Fig.02: How do I show/list installed packages in Alpine Linux](https://www.cyberciti.biz/media/new/faq/2017/05/apk-list-installed-packages.jpg)

Fig.02: How do I show/list installed packages in Alpine Linux

### Find out which package a file belongs to..

to determine which package a file named /etc/passwd or /sbin/apk belongs to:  
`# **apk info --who-owns /etc/passwd**  
/etc/passwd is owned by alpine-baselayout-3.0.4-r0  
# **apk info --who-owns /sbin/apk**  
/sbin/apk is owned by apk-tools-2.6.8-r2`

### List contents of the PACKAGE

`# apk -L info pkgName  
# apk -L info htop`  
Sample outputs:

htop-2.0.2-r0 contains:
usr/bin/htop
usr/share/applications/htop.desktop
usr/share/pixmaps/htop.png

### Check if PACKAGE is installed

`# apk -e info pkgName  
#############################################  
### find out if atop PACKAGE is installed ###  
#############################################  
# apk -e info atop`  
No output displayed if PACKAGE is NOT installed.

### List packages that the PACKAGE depends on

`# apk -R info atop  
# apk -R info atop`  
Sample outputs:

atop-2.2\_p3-r0 depends on:
so:libc.musl-x86\_64.so.1
so:libncursesw.so.6
so:libz.so.1

### List all packages depending on PACKAGE

`# apk info -r pkgName  
# apk info -r bash`  
Sample outputs:

bash-completion-2.4-r0

### Show installed size of PACKAGE

`# apk info -s pkgName  
# apk info -s atop`  
Sample outputs:

atop-2.2\_p3-r0 installed size:
520192

### Print description for PACKAGE

`# apk info -d pkgName  
# apk info -d bash`  
Sample outputs:

bash-4.3.46-r5 description:
The GNU Bourne Again shell

### Print all information about PACKAGE

`# apk info -a pkgName  
# apk info -a bash`  
Sample outputs:

apk info -a bash
bash-4.3.46-r5 description:
The GNU Bourne Again shell

bash-4.3.46-r5 webpage:
http://www.gnu.org/software/bash/bash.html

bash-4.3.46-r5 installed size:
700416

bash-4.3.46-r5 depends on:
busybox
so:libc.musl-x86\_64.so.1
so:libncursesw.so.6
so:libreadline.so.6

bash-4.3.46-r5 provides:

bash-4.3.46-r5 is required by:
bash-completion-2.4-r0

bash-4.3.46-r5 contains:
bin/bashbug
bin/bash

bash-4.3.46-r5 triggers:

bash-4.3.46-r5 has auto-install rule:

bash-4.3.46-r5 affects auto-installation of:
bash-doc-4.3.46-r5

bash-4.3.46-r5 replaces:

bash-4.3.46-r5 license:
GPL3+

## How do I see statistics about repositories and installations?

Run the command:  
`# apk stats`  
Sample outputs:

installed:
  packages: 28
  dirs: 163
  files: 7097
  bytes: 41205760
  triggers: 1
available:
  names: 11710
  packages: 7961
atoms:
  num: 5934
bash-4.3# 
bash-4.3# apk stats
installed:
  packages: 28
  dirs: 163
  files: 7097
  bytes: 41205760
  triggers: 1
available:
  names: 11710
  packages: 7961
atoms:
  num: 5934

## apk command options and examples

Command

Usage

Example

apk update

Update the package list

apk update

apk upgrade

Upgrade the system

apk update  
apt ugrade

apk add pkg

Add a package

apk add apache

apk del pkg

Delete a package

apk del nginx

apk search -v

Search for packages

apk search -v  
apk search -v -d ‘nginx\*’  
apk search -v ‘apache\*’

apk info

List all installed pacakges

apk info

apk fix

Repair package or upgrade it without modifying main dependencies

apk fix

apk policy pkg

Show repository policy for packages

apk policy bash

apk stats

Show statistics about repositories and installations

apk stats

##### See also

-   **/etc/apk/repositories** file.
-   apk man page

  
  

Category

List of Unix and Linux commands

File Management

[cat](https://www.cyberciti.biz/faq/linux-unix-appleosx-bsd-cat-command-examples/ "cat command examples and syntax") • [ncdu](https://www.cyberciti.biz/open-source/install-ncdu-on-linux-unix-ncurses-disk-usage/ "ncdu command examples and syntax")

Firewall

[Alpine Awall](https://www.cyberciti.biz/faq/how-to-set-up-a-firewall-with-awall-on-alpine-linux/ "Awall firewall on Alpine Linux examples and syntax") • [CentOS 8](https://www.cyberciti.biz/faq/how-to-set-up-a-firewall-using-firewalld-on-centos-8/ "firewalld on CentOS 8 examples and syntax") • [OpenSUSE](https://www.cyberciti.biz/faq/set-up-a-firewall-using-firewalld-on-opensuse-linux/ "firewalld on OpenSUSE Linux examples and syntax") • [RHEL 8](https://www.cyberciti.biz/faq/configure-set-up-a-firewall-using-firewalld-on-rhel-8/ "firewalld on RHEL (Red Hat Enterprise Linux) 8 examples and syntax") • [Ubuntu 16.04](https://www.cyberciti.biz/faq/howto-configure-setup-firewall-with-ufw-on-ubuntu-linux/ "ufw on Ubuntu 16.04 LTS examples and syntax") • [Ubuntu 18.04](https://www.cyberciti.biz/faq/how-to-setup-a-ufw-firewall-on-ubuntu-18-04-lts-server/ "ufw on Ubuntu 18.04 LTS examples and syntax") • [Ubuntu 20.04](https://www.cyberciti.biz/faq/how-to-configure-firewall-with-ufw-on-ubuntu-20-04-lts/ "ufw on Ubuntu 20.04 LTS examples and syntax")

Network Utilities

[NetHogs](https://www.cyberciti.biz/faq/linux-find-out-what-process-is-using-bandwidth/ "NetHogs - Monitor per process network bandwidth usage under Linux examples and syntax") • [dig](https://www.cyberciti.biz/faq/linux-unix-dig-command-examples-usage-syntax/ "dig command examples and syntax") • [host](https://www.cyberciti.biz/faq/linux-unix-host-command-examples-usage-syntax/ "host command examples and syntax") • [ip](https://www.cyberciti.biz/faq/linux-ip-command-examples-usage-syntax/ "ip command in Linux examples and syntax") • [nmap](https://www.cyberciti.biz/security/nmap-command-examples-tutorials/ "nmap command in Linux examples and syntax")

OpenVPN

[CentOS 7](https://www.cyberciti.biz/faq/centos-7-0-set-up-openvpn-server-in-5-minutes/ "CentOS 7 Set Up OpenVPN Server In 5 Minutes examples and syntax") • [CentOS 8](https://www.cyberciti.biz/faq/centos-8-set-up-openvpn-server-in-5-minutes/ "CentOS 8 OpenVPN server in 5 mintues examples and syntax") • [Debian 10](https://www.cyberciti.biz/faq/debian-10-set-up-openvpn-server-in-5-minutes/ "Debian 10 Set Up OpenVPN Server In 5 Minutes examples and syntax") • [Debian 8/9](https://www.cyberciti.biz/faq/install-configure-openvpn-server-on-debian-9-linux/ "OpenVPN server on Debian 9/8 examples and syntax") • [Ubuntu 18.04](https://www.cyberciti.biz/faq/ubuntu-18-04-lts-set-up-openvpn-server-in-5-minutes/ "Ubuntu 18.04 LTS Set Up OpenVPN Server In 5 Minutes examples and syntax") • [Ubuntu 20.04](https://www.cyberciti.biz/faq/ubuntu-20-04-lts-set-up-openvpn-server-in-5-minutes/ "Ubuntu 20.04 LTS OpenVPN server in 5 mintues examples and syntax")

Package Manager

apk • [apt](https://www.cyberciti.biz/faq/ubuntu-lts-debian-linux-apt-command-examples/ "apt command in Debian/Ubuntu Linux examples and syntax")

Processes Management

[bg](https://www.cyberciti.biz/faq/unix-linux-bg-command-examples-usage-syntax/ "bg command examples and syntax") • [chroot](https://www.cyberciti.biz/faq/unix-linux-chroot-command-examples-usage-syntax/ "chroot command examples and syntax") • [cron](https://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/ "cron and crontab command examples and syntax") • [disown](https://www.cyberciti.biz/faq/unix-linux-disown-command-examples-usage-syntax/ "disown command examples and syntax") • [fg](https://www.cyberciti.biz/faq/unix-linux-fg-command-examples-usage-syntax/ "fg command examples and syntax") • [jobs](https://www.cyberciti.biz/faq/unix-linux-jobs-command-examples-usage-syntax/ "jobs command examples and syntax") • [killall](https://www.cyberciti.biz/faq/unix-linux-killall-command-examples-usage-syntax/ "killall command examples and syntax") • [kill](https://www.cyberciti.biz/faq/unix-kill-command-examples/ "kill command examples and syntax") • [pidof](https://www.cyberciti.biz/faq/linux-pidof-command-examples-find-pid-of-program/ "pidof command examples and syntax") • [pstree](https://www.cyberciti.biz/faq/unix-linux-pstree-command-examples-shows-running-processestree/ "pstree command examples and syntax") • [pwdx](https://www.cyberciti.biz/faq/unix-linux-pwdx-command-examples-usage-syntax/ "pwdx command examples and syntax") • [time](https://www.cyberciti.biz/faq/unix-linux-time-command-examples-usage-syntax/ "time command examples and syntax")

Searching

[grep](https://www.cyberciti.biz/faq/howto-use-grep-command-in-linux-unix/ "grep command examples and syntax") • [whereis](https://www.cyberciti.biz/faq/unix-linux-whereis-command-examples-to-locate-binary/ "whereis command examples and syntax") • [which](https://www.cyberciti.biz/faq/unix-linux-which-command-examples-syntax-to-locate-programs/ "which command examples and syntax")

User Information

[groups](https://www.cyberciti.biz/faq/unix-linux-groups-command-examples-syntax-usage/ "groups command examples and syntax") • [id](https://www.cyberciti.biz/faq/unix-linux-id-command-examples-usage-syntax/ "id command examples and syntax") • [lastcomm](https://www.cyberciti.biz/faq/linux-unix-lastcomm-command-examples-usage-syntax/ "lastcomm command examples and syntax") • [last](https://www.cyberciti.biz/faq/linux-unix-last-command-examples/ "last command examples and syntax") • [lid/libuser-lid](https://www.cyberciti.biz/faq/linux-lid-command-examples-syntax-usage/ "lid/libuser-lid command examples and syntax") • [logname](https://www.cyberciti.biz/faq/unix-linux-logname-command-examples-syntax-usage/ "longname command examples and syntax") • [members](https://www.cyberciti.biz/faq/linux-members-command-examples-usage-syntax/ "members command examples and syntax") • [users](https://www.cyberciti.biz/faq/unix-linux-users-command-examples-syntax-usage/ "users command examples and syntax") • [whoami](https://www.cyberciti.biz/faq/unix-linux-whoami-command-examples-syntax-usage/ "whoami command examples and syntax") • [who](https://www.cyberciti.biz/faq/unix-linux-w-command-examples-syntax-usage-2/ "who command examples and syntax") • [w](https://www.cyberciti.biz/faq/unix-linux-w-command-examples-syntax-usage-2/ "w command examples and syntax")

WireGuard VPN

[Alpine](https://www.cyberciti.biz/faq/how-to-set-up-wireguard-vpn-server-on-alpine-linux/ "Alpine Linux set up WireGuard VPN server examples and syntax") • [CentOS 8](https://www.cyberciti.biz/faq/centos-8-set-up-wireguard-vpn-server/ "CentOS 8 set up WireGuard VPN server examples and syntax") • [Debian 10](https://www.cyberciti.biz/faq/debian-10-set-up-wireguard-vpn-server/ "Debian 10 set up WireGuard VPN server examples and syntax") • [Firewall](https://www.cyberciti.biz/faq/how-to-set-up-wireguard-firewall-rules-in-linux/ "WireGuard Firewall Rules in Linux examples and syntax") • [Ubuntu 20.04](https://www.cyberciti.biz/faq/ubuntu-20-04-set-up-wireguard-vpn-server/ "Ubuntu 20.04 set up WireGuard VPN server examples and syntax")