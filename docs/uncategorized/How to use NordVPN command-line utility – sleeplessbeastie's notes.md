Use NordVPN command-line utility to easily manage VPN service.

### Installation

Install required utilities.

$ sudo apt install wget apt-transport-https

Download package that contains NordVPN repository configuration.

$ wget --directory-prefix /tmp https://repo.nordvpn.com/deb/nordvpn/debian/pool/main/nordvpn-release\_1.0.0\_all.deb

This package contains repository definition and the public key used to sign package index. Unfortunately, this is the only way to get the public key as it is not available in any other way.

Install the downloaded package.

$ sudo apt install /tmp/nordvpn-release\_1.0.0\_all.deb

Update package index.

$ sudo apt update

Install `nordvpn` utility.

$ sudo apt install nordvpn

### Usage

Display usage information.

$ nordvpn help

Welcome to NordVPN Linux client app!
Version 2.2.0-0
Website: https://nordvpn.com
Usage: nordvpn \[global options\] command \[command options\] \[arguments...\]
Commands:
 login          Logs you in
 logout         Logs you out
 connect, c     Connects you to VPN
 disconnect, d  Disconnects you from VPN
 status         Shows the connection status
 set            Sets a configuration option
 whitelist      Adds or removes option from whitelist
 settings       Shows the current settings
 countries      Shows the country list
 cities         Shows the city list
 help, h        Shows a list of commands or help for one command
Global options:
 --help, -h     show help
 --version, -v  print the version
For more detailed information, please check manual page.
Our customer support works 24/7 so if you have any questions or issues, drop us a line at https://support.nordvpn.com/

Provide user credentials to log you in.

$ nordvpn login

Please enter your login details.
Email / Username: \*\*\*\*\*\*\*\*\*@\*\*\*\*\*\*\*\*\*.\*\*\*
Password:         \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
You are logged in. Welcome to NordVPN! You can now connect via 'nordvpn connect'.

Connect to the VPN service.

$ nordvpn connect

Connecting to United States #2109 (us2109.nordvpn.com)
Great! You are now connected to United States #2109 (us2109.nordvpn.com)

Disconnect from service.

$ nordvpn disconnect

You have been disconnected from NordVPN.

Display settings usage information.

$ nordvpn set help

Welcome to NordVPN Linux client app!
Version 2.2.0-0
Website: https://nordvpn.com
Usage: nordvpn set \[global options\] command \[command options\] \[arguments...\]
Commands:
     protocol     Sets the protocol.
     killswitch   Enables or disables Kill Switch. This security feature blocks your device from accessing the Internet outside the secure VPN tunnel, in case connection with a VPN server is lost.
     cybersec     Enables or disables CyberSec. When enabled, the CyberSec feature will automatically block suspicious websites so that no malware or other cyber threats can infect your device. Additionally, no flashy ads will come into your sight. More information on how it works: https://nordvpn.com/features/cybersec/.
     autoconnect  Enables or disables auto connect. When enabled, this feature will automatically try to connect to VPN on operating system startup.
     obfuscate    Enables or disables obfuscation. When enabled, this feature allows to bypass network traffic sensors which aim to detect usage of the protocol and log, throttle or block it.
     dns          Sets DNS servers
Global options:
   --help, -h  show help
For more detailed information, please check manual page.
Our customer support works 24/7 so if you have any questions or issues, drop us a line at https://support.nordvpn.com/

Define protocol to use (UDP/TCP).

$ nordvpn set protocol udp

Protocol is successfully set to 'UDP'.

Enable or disable kill switch.

$ nordvpn set killswitch enable

Kill Switch is successfully set to 'enabled'.

Enable or disable [CyberSec](https://nordvpn.com/features/cybersec/).

$ nordvpn set cybersec disable

CyberSec is already set to 'disabled'.

Enable or disable obfuscation.

$ nordvpn set obfuscate disable

Obfuscation is already set to 'disabled'.

Enable or disable connection on system startup.

$ nordvpn set autoconnect enable

Auto connect is successfully set to 'enabled'

Set a specific DNS server.

$ nordvpn set dns 1.1.1.1 8.8.8.8

DNS is successfully set to '1.1.1.1 8.8.8.8'.

Disable custom DNS server.

$ nordvpn set dns disable

DNS is successfully set to 'disabled'.

Open port on the firewall.

$ nordvpn whitelist add port 22 protocol tcp

Port 22 (TCP) successfully whitelisted.

Close opened port on the firewall.

$ nordvpn whitelist remove port 80 protocol tcp

Port 80 (TCP) successfully removed from whitelist.

Display settings.

$ nordvpn settings

Protocol: UDP
Kill Switch: enabled
CyberSec: disabled
Obfuscate: disabled
Auto connect: enabled
DNS: disabled
Whitelisted ports:
        22 (TCP)

Display available countries.

$ nordvpn countries

Albania                 Germany                 Poland
Argentina               Greece                  Portugal
Australia               Hong\_Kong               Romania
Austria                 Hungary                 Russia
Azerbaijan              Iceland                 Serbia
Belgium                 India                   Singapore
Bosnia\_And\_Herzegovina  Indonesia               Slovakia
Brazil                  Ireland                 Slovenia
Bulgaria                Israel                  South\_Africa
Canada                  Italy                   South\_Korea
Chile                   Japan                   Spain
Costa\_Rica              Latvia                  Sweden
Croatia                 Luxembourg              Switzerland
Cyprus                  Macedonia               Taiwan
Czech\_Republic          Malaysia                Thailand
Denmark                 Mexico                  Turkey
Estonia                 Moldova                 Ukraine
Finland                 Netherlands             United\_Kingdom
France                  New\_Zealand             United\_States
Georgia                 Norway                  Vietnam

Display cities in a specific country.

$ nordvpn cities Germany

Berlin          Frankfurt

Connect to VPN service using a specific location.

$ nordvpn connect Germany Frankfurt

Connecting to Germany #343 (de343.nordvpn.com)
Great! You are now connected to Germany #343 (de343.nordvpn.com)

Display connection status.

$ nordvpn status

Status: Connected
Current server: de343.nordvpn.com
Country: Germany
City: Frankfurt
Your new IP: 185.216.33.13
Current protocol: UDP
Transfer: 5.4 KiB received, 1.9 KiB sent
Uptime: 15 seconds

Remove provided credentials to log you out.

$ nordvpn logout

You have been logged out.

### Additional information

Display firewall configuration defined by the service.

$ sudo iptables -L -v -n

Chain INPUT (policy DROP 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
   15  5122 ACCEPT     all  --  tun0   \*       0.0.0.0/0            0.0.0.0/0            ctstate RELATED,ESTABLISHED
    0     0 ACCEPT     all  --  lo     \*       31.13.191.176        0.0.0.0/0            ctstate RELATED,ESTABLISHED
    0     0 ACCEPT     all  --  lo     \*       127.0.0.0/8          0.0.0.0/0            ctstate RELATED,ESTABLISHED
   32 11972 ACCEPT     all  --  enp0s3 \*       31.13.191.176        0.0.0.0/0            ctstate RELATED,ESTABLISHED
   99  7392 ACCEPT     all  --  enp0s3 \*       192.168.88.0/24      0.0.0.0/0            ctstate RELATED,ESTABLISHED
    0     0 ACCEPT     all  --  tun0   \*       31.13.191.176        0.0.0.0/0            ctstate RELATED,ESTABLISHED
    0     0 ACCEPT     all  --  tun0   \*       10.8.0.0/16          0.0.0.0/0            ctstate RELATED,ESTABLISHED
    0     0 ACCEPT     all  --  lo     \*       0.0.0.0/0            0.0.0.0/0
    0     0 ACCEPT     tcp  --  lo     \*       127.0.0.0/8          0.0.0.0/0            tcp dpt:22
    0     0 ACCEPT     tcp  --  enp0s3 \*       192.168.88.0/24      0.0.0.0/0            tcp dpt:22
    0     0 DROP       all  --  \*      \*       127.0.0.0/8          0.0.0.0/0
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
Chain OUTPUT (policy DROP 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
    0     0 ACCEPT     udp  --  \*      lo      0.0.0.0/0            1.1.1.1              udp dpt:53
    0     0 ACCEPT     udp  --  \*      lo      0.0.0.0/0            8.8.8.8              udp dpt:53
    2   152 ACCEPT     udp  --  \*      tun0    0.0.0.0/0            1.1.1.1              udp dpt:53
    0     0 ACCEPT     udp  --  \*      tun0    0.0.0.0/0            8.8.8.8              udp dpt:53
   18  1633 ACCEPT     all  --  \*      tun0    0.0.0.0/0            0.0.0.0/0
    0     0 ACCEPT     all  --  \*      lo      0.0.0.0/0            31.13.191.176
    0     0 ACCEPT     all  --  \*      lo      0.0.0.0/0            127.0.0.0/8
   21  2914 ACCEPT     all  --  \*      enp0s3  0.0.0.0/0            31.13.191.176
   59  7344 ACCEPT     all  --  \*      enp0s3  0.0.0.0/0            192.168.88.0/24
    0     0 ACCEPT     all  --  \*      tun0    0.0.0.0/0            31.13.191.176
    0     0 ACCEPT     all  --  \*      tun0    0.0.0.0/0            10.8.0.0/16
    0     0 ACCEPT     all  --  \*      lo      0.0.0.0/0            0.0.0.0/0

Display service configuration.

$ cat ~/.config/nordvpn/nordvpn.conf

{
  "id": 3012390686,
  "protocol": "udp",
  "kill\_switch": true,
  "cybersec": false,
  "obfuscate": true,
  "dns": \[
    "1.1.1.1",
    "8.8.8.8"
  \],
  "whitelist": {
    "tcp": \[
      22
    \]
  }
}

Display DNS configuration.

$ cat /etc/resolv.conf

\# Generated by NordVPN
nameserver 1.1.1.1
nameserver 8.8.8.8

Display service status.

$ systemctl status nordvpnd

● nordvpnd.service - NordVPN Daemon
   Loaded: loaded (/etc/systemd/system/nordvpnd.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2019-01-14 23:38:47 CET; 59min ago
 Main PID: 379 (nordvpnd)
    Tasks: 10 (limit: 1152)
   Memory: 288.3M
   CGroup: /system.slice/nordvpnd.service
           ├─ 379 /usr/sbin/nordvpnd
           └─3418 /var/lib/nordvpn/openvpn --config /tmp/nordvpn-ovpn377746007 --management /var/run/nordvpn-openvpn.sock unix --redirect-gateway --script-security 1 --connect-retry 5 5 --auth-retry nointeract --management-query-passwords