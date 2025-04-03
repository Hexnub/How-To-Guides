# NTP - A How To Guide by Hexnub

## NTP Server

## How to create and configure an NTP server
1. On Ubuntu update your local repo and upgrade if you wish.
```bash
sudo apt update && sudo apt upgrade -y
```
2. Install the ntpd daemon which will serve as both ntp server and client.
```bash
sudo apt install ntp
```
3. Configuring the ntp configuration file
open the file with your favorite text editor. I use vim
```bash
sudo vim /etc/ntpsec/ntp.conf
```
the ntp.conf file contain pre-configured server pools, however it would be best to use local pool for less latency, visit the ntp pool project website for details.
```
https://www.ntppool.org/zone/us
```
replace the pool entries with your local pool
```
server 0.us.pool.ntp.org
server 1.us.pool.ntp.org
server 2.us.pool.ntp.org
server 3.us.pool.ntp.org
```
if you already have a server with a lower Stratum number (higher tier ntp) and wish to sync this server with this local ntp add the ip address and or hostname of your ntp server to this file replacing the pool information.
```
server ntp.domaincontroller.com prefer
server 10.10.1.3
```
restart the ntp service for the changes to take effect. 
```bash
sudo systemctl restart ntp
```
check your ntp sources
```bash
ntpq -p
```
Note: restart the ntp daemon after making any changes to the ntp.conf file
```bash
sudo systemctl restart ntp
```

## Setting the time zone with timedatectl
List available timezones
```bash
timedatectl list-timezones
```
Set timezone
```bash
sudo timedatectl set-timezone America/Los_Angeles
```
Verify timezone
```bash
timedatectl
```

