# Intro to Networking
## The OSI Model: An Overview
The OSI (Open Systems Interconnection) Model is a seven-layer conceptual framework used to understand and design networks. While TCP/IP is used in the real world, OSI is an excellent model for learning and organizing the structure of networking.

### The Seven Layers:
1. Physical
Deals with the actual hardware, binary transmission, and physical signal sending.

2. Data Link
Focuses on physical (MAC) addressing, formatting data into frames, and error checking. Adds MAC address info from the NIC. Includes a trailer to check for data corruption.

5. Network
Responsible for logical addressing using IP addresses. Determines the best route for data. Works with protocols like IPv4 and IPv6.

4. Transport
Chooses between TCP (reliable, connection-oriented) or UDP (faster, connectionless). Breaks transmissions into segments (TCP) or datagrams (UDP).

5. Session
Establishes, maintains, and terminates communication sessions. Allows multiple simultaneous sessions (like browser tabs) to remain distinct.

6. Presentation
Translates data into a standardized format. Handles compression, encryption, and encoding.

7. Application
Provides network access to applications (like web browsers). Interfaces directly with the software requesting network services.

Mnemonic used:
All People Seem To Need Data Protection

## Encapsulation and De-Encapsulation
As data moves down the OSI model, headers and (in some cases) trailers are added at each layer. This process is called encapsulation. Each layer's header adds essential information such as:

- IP addresses (Network layer)

- Protocol and port info (Transport layer)

- Error-checking trailer (Data Link layer)

At the receiving end, the data moves back up through each layer in de-encapsulation, with each layer removing its relevant header/trailer. This standardized process ensures reliable communication between systems regardless of the manufacturer.

## OSI Data Names by Layer:
- Layers 5–7: Data

- Layer 4: Segments (TCP) / Datagrams (UDP)

- Layer 3: Packets

- Layer 2: Frames

- Layer 1: Bits

## The TCP/IP Model
A four-layer model based on real-world networking. While simpler than OSI, it maps closely:

4. Application
Covers OSI’s Application, Presentation, and Session layers

3. Transport
Equivalent to OSI’s Transport layer

2. Internet
Matches OSI’s Network layer

1. Network Interface
Covers OSI’s Data Link and Physical layers

Some resources break Network Interface into two layers, making it a five-layer model.

## TCP and the Three-Way Handshake
TCP forms connections using a three-step process:

1. Client sends SYN

2. Server replies with SYN-ACK

3. Client replies with ACK

Once complete, data can be sent reliably. Lost data is re-sent. This handshake ensures stability and connection integrity.

The TCP/IP model was developed by the US Department of Defense in 1982 to standardize networking. While OSI followed later as a more comprehensive teaching tool, TCP/IP remains the operational standard.

## Key Tools and Protocols
### ping
Used to check if a remote host is reachable. Works over ICMP, which sits in the Network layer (OSI) or Internet layer (TCP/IP).

Example:
ping google.com
Returns IP address and latency results. Universally supported by most operating systems.

### traceroute / tracert
Maps the path data takes across a network to reach a destination. Useful for identifying routing issues.

- traceroute (Linux/Unix)

- tracert (Windows)

Uses UDP on Unix, ICMP on Windows.

### whois
Checks domain registration details including owner, registrar, and more.

Basic usage:
whois <domain>

To install on Debian-based systems:
sudo apt update && sudo apt-get install whois

### dig
Queries DNS servers for information about domain name resolution. Helpful for troubleshooting and understanding DNS flow.

Syntax:
dig <domain> @<dns-server-ip>

Focus on the ANSWER section for the returned IP address and the TTL (time to live), which tells how long to cache the result.

## DNS Resolution Process Overview:
1. Check local hosts file

2. Check DNS cache

3. Ask recursive DNS server (usually via router or ISP)

4. If not cached, request goes to a root name server

5. Then to the appropriate TLD server (.com, .net, etc.)

6. Finally to the authoritative name server which contains the DNS records for the requested domain

Each step narrows down the destination until the actual IP is returned.
