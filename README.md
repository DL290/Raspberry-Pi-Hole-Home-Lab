# Raspberry-Pi-Hole-Home-Lab
Raspberry Pi 5 network wide DNS filtering and Linux hole lab. 

Project Overview 
The project consisted of deploying a network wide DNS filtering solution using the Pi-Hole software hosted on a Raspberry Pi 5. The project started by imaging my Raspberry Pi 5 with Linux and completing the entire project via SSH. 

Objective
The main objective was to gain hands on experience with Linux systems administration, DNS infrastructure, home networking and network security. 

Hardware and Software: 
Component                Configuration 
Computer               Paspberry Pi 5 
Memory                 4GB RAM 
Storage                32 GB Micro SD 
Operating system       Raspberry Pi OS 
Network Connection     Ethernet 
DNS Filtering          Pi-hole
Router                 Century Link C4000XG 
Remote Administration  SSH 
Upstream DNS           Cloudflare 

Network Architecture 
The CenturyLink router distributes the Raspberry Pi's reserved local IP address as the DNS server through DHCP.
DNS requests from participating network devices are forwarded to Pi-hole. Pi-hole checks requested domains against its blocklists and forwards permitted DNS queries to an upstream resolver.

DNS request flow: 
Client -> Router / DHCP Configuration -> Raspberry Pi / Pi-Hole -> Upstream DNS 
BLOCKED domains are not forwarded for normal resolution 

Implementation Steps 
1. Raspberry Pi Configuration
   Install Raspberry Pi OS
   Configure headless administration through SSH
   Update system packages
   Install active cooling
   Configure Pi to run via ethernet

2. Network Configuration
   Identify the router's local gateway
   Configure a DHCP reservation for the Raspberry Pi
   Migrate the Raspberry Pi from Wi-Fi to Ethernet
   Configure custom DNS settings on the CenturyLink router 
 
3. Pi-Hole Deployment
   Install Pi-Hole using the official installer 
   Configure upstream DNS resolution
   Enable a default domain blocklist
   Configure the web administration interface
   Applied privacy settings to limit collection of client DNS activity

4. Testing and Validation
   Verified normal DNS resolution using: nslookup google.com <PIHOLE_IP>
   Verified DNS blocking using: nslookup doubleclick.net <PIHOLE_IP>
   The blocking test returned 0.0.0.0 and ::, confirming that Pi-hole was filtering the requested domain.

Troubleshooting and Lessons Learned: 
DHCP reservations: Wi-Fi and Ethernet use different MAC addresses, requiring separate DHCP reservations and Pi-hole configuration 
Connectivity: Confirmed that switching from Wi-Fi to Ethernet changed the Raspberry Pi's network address and required reconnecting SSH.
Availability: Learned that using a single Pi-hole server for network-wide DNS creates a potential single point of failure.
Privacy: Configured Pi-hole to minimize the visibility and retention of household DNS query activity.

Project Notes: 
This project documents the deployment and administration of the open-source Pi-hole application. Pi-hole itself was developed by the Pi-hole project.
Actual network addresses, hardware identifiers, authentication details, and private DNS query records have been redacted from this public repository. 

## Pi-hole Dashboard

The dashboard below shows my Raspberry Pi 5 actively processing and filtering DNS requests across my home network.

![Pi-hole Dashboard](Pi-Hole%20screenshot.png)
