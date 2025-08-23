# Networking Secure Protocols
## Summary
In the Networking Secure Protocols room, I learned how security is added to core protocols to protect confidentiality, integrity, and authenticity. 
Without this protection, attackers could read sensitive data (like passwords or credit cards), alter transactions, or impersonate legitimate servers.

TLS is layered onto protocols like HTTP, SMTP, POP3, and IMAP, transforming them into their secure versions (HTTPS, SMTPS, POP3S, IMAPS). SSH was 
introduced as a secure replacement for Telnet, and VPNs provide a way to build secure networks over insecure ones.

### Key objectives covered in this room:

- SSL/TLS and its role in securing communications

- Securing plaintext protocols (HTTP, SMTP, POP3, IMAP)

- Why SSH replaced Telnet

- How VPNs create secure channels over untrusted networks

## TLS (Transport Layer Security)

### Purpose: 
Encrypts data between a client and server for confidentiality and integrity; prevents eavesdropping and tampering.

### History:

- 1990s: SSL developed by Netscape

- 1999: TLS 1.0 replaced SSL 3.0

- 2018: TLS 1.3 released

### How it works:

1. Server generates a Certificate Signing Request (CSR)

2. CSR sent to Certificate Authority (CA)

3. CA verifies and issues a signed digital certificate

4. Clients validate the certificate using installed CA certificates

- TLS-secured protocols: HTTP → HTTPS, SMTP → SMTPS, POP3 → POP3S, IMAP → IMAPS, DNS → DoT

## HTTPS (HTTP over TLS)

- HTTP: Cleartext communication over TCP port 80

- HTTPS: Encrypted communication over TCP port 443

- Steps for HTTPS:

1. TCP handshake

2. TLS session negotiation

3. HTTP communication encrypted inside TLS

### Key takeaway: 
TLS doesn’t change HTTP; it just encrypts it, keeping lower layers (TCP/IP) unchanged

## Secure Email Protocols (TLS-secured)
Protocol - Default Port - Secure Version - Secure Port
- SMTP - 25 - SMTPS - 465
- POP3 - 110 - POP3S - 995
- IMAP - 143 - IMAPS - 993

- Works the same way as HTTPS: encrypts existing protocol traffic

## SSH (Secure Shell)

### Purpose: 
Replaces TELNET for secure remote access; encrypts login credentials and session data

### History:
- 1995: SSH-1 released

- 1996: SSH-2 defined

- OpenSSH open-source version widely used today

### Benefits:
- Secure authentication (password, public key, 2FA)

- Confidentiality and integrity of data

- Tunneling and X11 forwarding for GUI applications

### Usage: ssh username@hostname (port 22)
- Secure File Transfer

## SFTP and FTPS
- SFTP (SSH File Transfer Protocol): Uses SSH (port 22), Unix-like commands (get, put)

- FTPS (FTP Secure): FTP over TLS (port 990), requires certificates, uses separate control/data connections

## VPN (Virtual Private Network)
### Purpose: 
Creates a private, secure network over the public Internet

###Uses:
- Connect remote branches to main office

- Encrypt traffic and hide public IP

- Bypass geo-restrictions or local censorship

### Traffic routing:
- Full tunnel: all traffic goes through VPN

- Split tunnel: only specific traffic goes through VPN

- Precautions: Some VPNs leak IPs; some countries restrict VPN use

###Summary of Secure Networking Approaches
- TLS: Encrypts many protocols (HTTPS, SMTPS, POP3S, IMAPS)

- SSH: Secure remote access, file transfer, tunneling

- VPN: Connects networks securely, hides IP, encrypts traffic

### Wireshark TLS Decryption Example
- Log TLS keys in Chromium:

chromium --ssl-key-log-file=~/ssl-key.log

- Load ssl-key.log in Wireshark to decrypt TLS traffic and inspect contents


Wireshark TLS Decryption Example

Log TLS keys in Chromium by adding the option: chromium --ssl-key-log-file=~/ssl-key.log

Load ssl-key.log in Wireshark to decrypt TLS traffic and inspect contents
