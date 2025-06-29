# Networking Concepts - Notes
This lesson covered core concepts behind how devices communicate over networks, with a strong focus on both theoretical models and practical details. These fundamentals are crucial in both offensive and defensive cybersecurity work.

## OSI Model
The OSI (Open Systems Interconnection) model is a conceptual framework developed by the ISO to understand how network communication occurs in seven layers:

Physical

Transmits raw data via physical media (cables, antennas).

Defines binary representation and transmission.

Data Link

Provides communication between devices on the same network (e.g. a switch).

Deals with MAC addresses (e.g. a4:c3:f0:85:ac:2d).

Examples: Ethernet (802.3), WiFi (802.11).

Network

Routes data between different networks.

Logical addressing and routing take place here.

Examples: IP, ICMP, VPN protocols (IPSec, SSL/TLS).

Transport

End-to-end communication between applications.

Examples: TCP (reliable), UDP (unreliable).

Session

Establishes, maintains, and synchronizes sessions between applications.

Examples: NFS, RPC.

Presentation

Formats and translates data for the application layer.

Handles encryption, encoding (ASCII, Unicode), and compression.

Example: MIME encoding for attachments.

Application

Directly interacts with user-facing applications.

Examples: HTTP, FTP, DNS, SMTP, IMAP.

## TCP/IP Model
The TCP/IP model was developed by the DoD and predates the OSI model. It has 4 layers (sometimes 5 with Physical included):

Application
Combines OSI layers 5–7.

Transport
Matches the OSI transport layer.

Internet
Handles logical addressing and routing (like OSI’s Network layer).

Link
Covers both physical and data link operations.

This model emphasizes resiliency and dynamic routing across the internet.

## IP Addresses and Subnets
IP addresses (e.g. 192.168.0.1) uniquely identify hosts on a network.

IPv4 addresses are composed of four octets (32 bits), allowing roughly 4.3 billion possible addresses.

The first and last IPs in a subnet (e.g. 192.168.1.0 and 192.168.1.255) are reserved for network and broadcast.

Subnet Masks
A subnet mask like 255.255.255.0 is represented as /24 (meaning 24 fixed bits).

/24 subnet allows host IPs from .1 to .254.

Private IP Ranges (RFC 1918)
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16

Private IPs are not routable over the public internet and require NAT (Network Address Translation) to access external networks.

Checking Network Configuration
Windows: ipconfig

Linux/macOS: ifconfig or ip a

This reveals:

Host IP address

Subnet mask

Broadcast address

## UDP and TCP
UDP (User Datagram Protocol)
Connectionless, fast but unreliable

No delivery acknowledgment

Uses port numbers (1–65535)

Real-world analogy: sending a letter without knowing if it arrived

TCP (Transmission Control Protocol)
Connection-oriented, reliable delivery

Uses sequence and acknowledgment numbers

Requires a three-way handshake to establish connection:

SYN (client → server)

SYN-ACK (server → client)

ACK (client → server)

## Encapsulation
Encapsulation adds headers (and sometimes trailers) as data moves through each layer:

Application Data

User inputs data (e.g. sends email)

Transport Segment

TCP or UDP adds transport headers

Network Packet

IP header is added

Data Link Frame

Ethernet/WiFi adds final header and trailer

At the destination, this process is reversed to extract the application data.

##Telnet
Telnet is a legacy protocol used to interact with remote systems over TCP. It can be used to test connections to specific ports. Although 
largely deprecated for secure access (due to lack of encryption), it remains useful for port testing and banner grabbing during reconnaissance.

Summary
This lesson provided a thorough walkthrough of network models, IP addressing, transport protocols, encapsulation, and key tools like Telnet. 
These concepts are foundational for nearly every area of cybersecurity, from blue team monitoring to red team enumeration.
