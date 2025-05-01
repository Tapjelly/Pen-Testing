# Week 12.1
## Configuring UFW
```console
cd Cybersecurity-Lesson-Plans/12-NetSec/
sudo docker-compose up -d
sudo docker exec -it ufw bash
sudo sed -i 's/^IPV6=.*/IPV6=no/' /etc/default/ufw
sudo service firewalld stop
sudo service firewalld status
# Now that we have UFW up and running we will attempt to SSH into firewalld container
ip addr show eth0
ssh sysadmin@172.16.180.72
exit
# We know that we can SSH into our UFW container which is an issue. Lets boot and configure our UFW firewall.
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
# lets add a rule to block the telnet port since it is a vulnerability
sudo ufw deny 23/tcp
# lets also allow the needed ports
sudo ufw allow 80 
sudo ufw allow 143 
sudo ufw allow 587
sudo ufw allow 110
sudo ufw allow 443
# lets finally reload the firewall to commit our changes
sudo ufw reload
# This stopped us from connecting via ssh but we can still connect if we do a telnet connection at port 80
telnet 172.16.180.72 80
```

## Configuring Firewalld
```console
# To begin we need to connect to the firewall container using docker
cd Cybersecurity-Lesson-Plans/12-NetSec/
sudo docker-compose up -d
sudo docker exec -it firewalld bash
# We must then use the following command to disable IPV6 on ufw to ensure firewalld can be configured properly
sudo sed -i 's/^IPV6=.*/IPV6=no/' /etc/default/ufw
# We will then remove ufw from this container and start firewalld
sudo apt remove ufw
service firewalld status
service firewalld start
# Next lets configure our firewall. First we list the zones.
firewall-cmd --get-zones
# We want to set eth0 to our home zone.
sudo firewall-cmd --zone=home --change-interface=eth0 --permanent
sudo firewall-cmd --reload
# We want to verify the change was successful
firewall-cmd --get-active-zones
# Lets list our active services in the home zone:
firewall-cmd --zone=home --list-services
# The output of this indicates that ssh, mdns, and dhcpv6-client are active.
# We will attempt to SSH into this container from out UFW container. This is successful but a telnet into this container fails indicating no route to the host.
# Although telnet fails due to not route when we ping the container we are able to successfully transmit data.
# Next lets block the UFWs IP.
sudo firewall-cmd --permanent --zone=home --add-rich-rule='rule family="ipv4" source address="172.16.180.72" reject'
# Now when we try to SSH into our firewalld container from our UFW container it fails because the IP is blocked.
```

## Testing Firewall Rules with nmap
```
Use nmap to perform network scans.
Use nmap -sO to perform an IP protocol scan.
Use nmap -sV to enumerate service type.
Use nmap -A -T4 to perform OS fingerprinting using fast execution.
Use uname -a to print the OS type and version.
Use nmap -sA to enumerate the type of firewall in use.
```

In this activity we will use Firewalld container to attack and the UFW as the victim.
```console
# Lets set up the victim machine
sudo ufw reset
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default deny outgoing
sudo ufw allow 80
sudo ufw allow 22
sudo ufw allow 443
# now we run a basic nmap to retrive some info
Starting Nmap 7.60 ( https://nmap.org ) at 2025-04-12 17:01 UTC
Nmap scan report for ufw.12-netsec_network_security_net (172.16.180.72)
Host is up (0.000064s latency).
Not shown: 997 filtered ports
PORT    STATE  SERVICE
22/tcp  open   ssh
80/tcp  open   http
443/tcp closed https
MAC Address: 02:42:AC:10:B4:48 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 12.55 seconds
# Next lets find out the service and daemon type
nmap -sV 172.16.180.72
Starting Nmap 7.60 ( https://nmap.org ) at 2025-04-12 17:04 UTC
Nmap scan report for ufw.12-netsec_network_security_net (172.16.180.72)
Host is up (0.000038s latency).
Not shown: 997 filtered ports
PORT    STATE  SERVICE VERSION
22/tcp  open   ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
80/tcp  open   http    nginx 1.14.0 (Ubuntu)
443/tcp closed https
MAC Address: 02:42:AC:10:B4:48 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.68 seconds
# Namp can do this because those ports are open, therefore we can probe them with protocol specific requests to create guesses to what services are running.
# Next lets do an OS fingerprint
nmap -A -T4
Starting Nmap 7.60 ( https://nmap.org ) at 2025-04-12 17:07 UTC
Nmap scan report for ufw.12-netsec_network_security_net (172.16.180.72)
Host is up (-0.018s latency).
Not shown: 997 filtered ports
PORT    STATE  SERVICE VERSION
22/tcp  open   ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 11:ae:b2:79:23:b4:8f:1a:5c:14:fe:d3:62:98:f2:64 (RSA)
|   256 08:44:55:77:01:65:72:eb:09:68:a0:82:b1:d6:8a:62 (ECDSA)
|_  256 73:8a:b0:d9:20:0f:4c:a1:ed:79:7c:3b:db:84:80:da (EdDSA)
80/tcp  open   http    nginx 1.14.0 (Ubuntu)
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: Welcome to nginx!
443/tcp closed https
MAC Address: 02:42:AC:10:B4:48 (Unknown)
Aggressive OS guesses: Linux 2.6.32 - 3.13 (95%), Linux 2.6.22 - 2.6.36 (93%), Linux 3.10 (93%), Linux 3.10 - 4.8 (93%), Linux 2.6.39 (93%), Linux 2.6.32 (92%), Linux 3.2 - 4.8 (92%), Linux 2.6.32 - 3.10 (91%), Linux 2.6.18 (91%), Linux 3.16 - 4.6 (91%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT ADDRESS
1   --  ufw.12-netsec_network_security_net (172.16.180.72)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.34 seconds
# Using uname -a on the victim machine we see that we are running Linux 5.15 which unfortunately was not in the agressive guesses this can be due to obfuscation or generic/misleading banners. We did however find MAC addresses.
# Lastly lets get info on the firewall
nmap -sA
Starting Nmap 7.60 ( https://nmap.org ) at 2025-04-12 17:12 UTC
Nmap scan report for ufw.12-netsec_network_security_net (172.16.180.72)
Host is up (-0.035s latency).
Not shown: 997 filtered ports
PORT    STATE      SERVICE
22/tcp  unfiltered ssh
80/tcp  unfiltered http
443/tcp unfiltered https
MAC Address: 02:42:AC:10:B4:48 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 12.43 seconds
# The behaviour of our firewall indicates it is host-based. We see ports are unfiltered. It is not a perimiter firewall but a private one on the UFW machine itself. It will operate on both Layer 3 and 4 of the OSI filering both IP and ports/protocols.
```
# Week 12.2 and 12.3
These activities will be uploaded as PDFs.
