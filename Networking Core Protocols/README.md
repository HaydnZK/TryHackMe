# Networking Core Protocols
## DNS: Remembering Addresses

The Domain Name System (DNS) allows us to use human-readable names instead of IP addresses. It operates at the application layer (Layer 7 of the OSI model) and typically uses UDP port 53, with TCP port 53 as a fallback.

Common DNS record types include:

- A Record: Maps a hostname to an IPv4 address.

- AAAA Record: Maps a hostname to an IPv6 address.

- CNAME Record: Maps a domain name to another domain name (example.com → www.example.com).

- MX Record: Specifies the mail server responsible for handling a domain’s email.

When a browser queries example.com, it looks up the A record. An email server, however, queries for the MX record. Command-line tools like nslookup can be used to test DNS queries.

Packet captures of DNS queries reveal requests and responses for both A and AAAA records, showing the client asking for addresses and the server responding with the mapped IPs.

## WHOIS

WHOIS records tell us who registered a domain and provide details like name, email, and address. Domain names are rented through registrars for one or more years, and whoever registers the domain has authority to set its DNS records.

WHOIS lookups can be done via web services or command-line tools. Privacy protection services can hide registrant information, but the underlying registration data is still maintained.

## HTTP(S): Accessing the Web

The Hypertext Transfer Protocol (HTTP) and its secure version (HTTPS) define how web browsers and servers communicate. They run on TCP, commonly using ports 80 or 8080 for HTTP and 443 or 8443 for HTTPS.

Common HTTP methods:

- GET: Retrieve data from the server.

- POST: Submit new data, such as forms.

- PUT: Create or overwrite resources.

- DELETE: Remove specified resources.

Wireshark captures show that browsers and servers exchange much more data than what is rendered to the user, including server versions and timestamps. HTTP can also be tested manually using telnet, sending lines like GET / HTTP/1.1 to retrieve pages directly.

## FTP: Transferring Files

The File Transfer Protocol (FTP) is designed specifically for transferring files and is often more efficient than HTTP. It listens on TCP port 21.

Key FTP commands:

- USER: Provide username.

- PASS: Provide password.

- RETR: Download a file from the server.

- STOR: Upload a file to the server.

Example process:

- Log in with the username anonymous.

- List files using ls (sent as LIST to the server).

- Switch modes with type ascii.

- Download a file with get filename.

FTP uses separate connections for commands and for data transfers like directory listings or file downloads.

## SMTP: Sending Email

The Simple Mail Transfer Protocol (SMTP) is used for sending emails. It runs on TCP port 25 and defines how mail clients and servers communicate.

Common SMTP commands:

- HELO / EHLO: Start a session.

- MAIL FROM: Define sender.

- RCPT TO: Define recipient.

- DATA: Provide message body.

- .: End the message.

An SMTP session can be demonstrated with telnet by manually issuing these commands, which shows the steps your email client normally automates.

## POP3: Receiving Email

The Post Office Protocol version 3 (POP3) is designed for downloading email messages to a local client. It uses TCP port 110 by default.

Common POP3 commands:

- USER: Identify user.

- PASS: Authenticate.

- STAT: Show number of messages and total size.

- LIST: List all messages.

- RETR: Retrieve a message.

- DELE: Delete a message.

- QUIT: End session.

POP3 is simple but downloads and removes messages from the server, making it better suited for single-device setups.

## IMAP: Synchronizing Email

The Internet Message Access Protocol (IMAP) is more advanced than POP3 and allows synchronization across multiple devices. Messages stay on the server and actions like moving, reading, or deleting are synced. IMAP uses TCP port 143.

Common IMAP commands:

- LOGIN: Authenticate.

- SELECT: Choose a mailbox.

- FETCH: Retrieve message headers or body.

- MOVE: Move messages between folders.

- COPY: Copy messages to another folder.

- LOGOUT: End session.

This protocol allows much greater flexibility and keeps emails consistent across all clients.

## Conclusion

A quick reference table of the protocols covered:

- TELNET: TCP 23

- DNS: UDP/TCP 53

- HTTP: TCP 80

- HTTPS: TCP 443

- FTP: TCP 21

- SMTP: TCP 25

- POP3: TCP 110

- IMAP: TCP 143
