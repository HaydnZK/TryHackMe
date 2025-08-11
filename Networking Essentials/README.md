# Networking Essentials

## Summary
This is the second in a series of four rooms about computer networking:

1. Networking Concepts

2. Networking Essentials (this room)

3. Networking Core Protocols

4. Networking Secure Protocols

### Learning Objectives
This room covers key protocols and technologies that “glue” networks together:

- Dynamic Host Configuration Protocol (DHCP)

- Address Resolution Protocol (ARP)

- Network Address Translation (NAT)

- Internet Control Message Protocol (ICMP)

- Ping

- Traceroute

## DHCP: Give Me My Network Settings
Devices need certain settings to connect to a network:

- IP address + subnet mask

- Router (gateway)

- DNS server

While servers often have manual static configurations, mobile devices benefit from automatic settings via DHCP (Dynamic Host Configuration Protocol).

DHCP is an application-level protocol that uses UDP:

- Server listens on UDP port 67

- Client sends from UDP port 68

Most smartphones and laptops use DHCP by default.

### DHCP DORA Process
DHCP uses a four-step process called DORA:

1. Discover: Client broadcasts DHCPDISCOVER to find DHCP servers.

2. Offer: Server replies with DHCPOFFER containing an available IP address.

3. Request: Client sends DHCPREQUEST accepting the offer.

4. Acknowledge: Server sends DHCPACK confirming the IP assignment.

### Example DHCP Exchange
Example tshark output of DHCP packets:

- Client broadcasts DHCP Discover from 0.0.0.0 to 255.255.255.255

- Server sends DHCP Offer to client IP

- Client sends DHCP Request from 0.0.0.0 to broadcast

- Server sends DHCP ACK confirming assignment

Notes:

- Client starts with no IP (0.0.0.0) and uses broadcast MAC address (ff:ff:ff:ff:ff:ff)

- After DHCP completes, the client receives:

1. Leased IP address

2. Gateway for routing outside local network

3. DNS server for domain name resolution

## ARP: Bridging Layer 3 Addressing to Layer 2 Addressing
Hosts communicate using IP packets (Layer 3) encapsulated in data link frames (Layer 2), like Ethernet or WiFi.

Even if a host knows the IP address of a target, it needs the target's MAC address to create a proper frame header.

### What is a MAC Address?
- 48-bit hardware address

- Usually represented in hexadecimal, e.g., 7C:DF:A1:D3:8C:5C

### ARP Overview
Address Resolution Protocol (ARP) finds the MAC address for a given IP on the same network.

Example ARP packets:

- Host with IP 192.168.66.89 broadcasts "Who has 192.168.66.1?" to MAC ff:ff:ff:ff:ff:ff

- Host with IP 192.168.66.1 replies with its MAC address

tcpdump output describes these as ARP Request and ARP Reply.

Note: ARP packets are encapsulated directly in Ethernet frames, not inside IP or UDP packets.

ARP is considered a Layer 2 protocol because it operates with MAC addresses but bridges Layer 3 addressing.

## ICMP: Troubleshooting Networks
Internet Control Message Protocol (ICMP) is used for network diagnostics and error reporting.

Two key tools using ICMP:

- Ping: Tests if a target is reachable by sending ICMP Echo Requests (Type 8) and waiting for Echo Replies (Type 0).

- Traceroute (Linux/UNIX) / Tracert (Windows): Discovers the path packets take by exploiting the TTL field.

### Ping Example
Ping sends 4 ICMP Echo Requests to a target IP and measures round-trip time (RTT). The output includes number of packets transmitted/received, loss percentage, and RTT stats.

### Traceroute Overview
- TTL limits how many routers a packet can pass.

- Each router decrements TTL by 1; when TTL hits zero, router drops the packet and sends an ICMP Time Exceeded (Type 11) message back.

- Traceroute sends packets with increasing TTLs to reveal each router along the path.

Notes:

- Some routers may not reply or block ICMP messages.

- Routing paths can change between traceroute runs.

## Routing
Routing decides how to forward packets from source to destination through networks.

Even simple networks need algorithms to determine the best paths.

Key routing protocols:

- OSPF (Open Shortest Path First): Shares network topology and calculates shortest paths dynamically.

- EIGRP (Enhanced Interior Gateway Routing Protocol): Cisco proprietary; selects paths based on metrics like bandwidth and delay.

- BGP (Border Gateway Protocol): Main routing protocol for the Internet; exchanges routing info between ISPs and large networks.

- RIP (Routing Information Protocol): Simple protocol for small networks; chooses routes based on the fewest hops.

## NAT: Network Address Translation
IPv4 supports about four billion addresses, but the growing number of devices required conservation methods.

NAT allows multiple devices on a private network to share a single public IP address.

- Private IPs inside the network map to a public IP for internet access.

- Routers supporting NAT maintain translation tables mapping internal IPs and ports to external IPs and ports.

Example:

- Laptop IP: 192.168.0.129, TCP source port 15401

- Internet server sees connection from router's public IP (e.g., 212.3.4.5) and port 19273
