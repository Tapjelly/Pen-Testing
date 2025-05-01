# Week 9.1
## DHCP Attacks
Refer to DHCPActivity.pcap <br>
In wireshark we can use the following filters:<br>
DHCP Discover = dhcp.option.dhcp == 1<br>
DHCP Offer = dhcp.option.dhcp == 2<br>
DHCP Request = dhcp.option.dhcp == 3<br>
DHCP ACK = dhcp.option.dhcp == 5<br>
Based on the packets in the network capture, we see a large number of Discover requests in a short period of time. This means we are faced with a DHCP starvation attack. 
This will result in the server running out of IP addresses to give to legitimate users.
We can also see the each request has a different MAC address meaning the attacker is likely spoofing their MAC address.

## Routing Schemes and Protocols
See file Week_9.1 RoutingSchemesAndProtocols.pdf

## Analyzing Wireless Security
Refer to wireless2.pcapng <br>
In this network Capture I can see 4 different wireless routers.<br>
BSSID                     SSID          Wireless Security<br>
00:01:e3:41:bd:6e         martinet3     WPA1<br>
00:0c:41:82:b2:55         Coherer       WPA1<br>
00:14:6c:7e:40:80         teddy         WPA1<br>
00:12:bf:12:32:29         Appart        WEP<br>
*Note: WEP is obselete and should not be used*

## Analyzing Wireless Attacks
Refer to kansascityWEP.pcap <br>
We need to decrypt this packet capture. Thankfully it was encrypted with WEP. We will use aircracker-ng to find the secret key. Key is 1F:1F:1F:1F:1F.
The security concern here is that it took us less than a minute to decrypt all of these packets through a dictionary attack. A more secure encryption protocol must be in place to secure sensitive data.

# Week 9.2
## DNS Record Types
We want to retrive the DNS records of namp.org. We want thier A records, NS records, SPF records, and MX records. <br>
nslookup -type=A namp.org<br>
This retrieves the name and IP address.<br>
nslookup -type=NS namp.org<br>
This retrieves the nameserver FQDN (Fully Qualified Domain Name) and nameserver IP address.<br>
nslookup -type=MX namp.org<br>
This retirves the mail exchanger record, the priority, and the hostname. The lower the number = the higher the priority. There needs to be muplite MX record for load balancing.<br>
nslookup -type=txt namp.org<br>
This specifies the renag of IPs allowed to send emails on behalf of nmap.org<br>

## Email Networking and Email Security
See file Week_9.2 EmailNetworking.pdf
## Network Concepts: Part 1
See file Week_9.2 NetworkingReviewPart1.pdf
## Network Concepts: Part 2
See file Week_9.2 NetworkingReviewPart2.pdf
