# Windows Command Line Basics
## Basic System Information
Use set to view environment variables, including the system PATH (where commands run from).

Find Windows version with the command:
ver
Example output:
Microsoft Windows [Version 10.0.20348.2655]

Get detailed system info, including hostname, by running:
systeminfo
Look for the Host Name field (e.g., WINSRV2022-CORE).

## Network Troubleshooting Commands
ipconfig — Shows IP info, subnet mask, gateway.
Use ipconfig /all for detailed info including DHCP status and lease times.

ping <target> — Tests connectivity by sending ICMP echo requests.

tracert <target> — Traces the route packets take to reach the target.

nslookup <domain> — Looks up domain name to IP.

netstat — Shows active connections and listening ports.
Useful flags:
-a (all connections & listening ports)
-b (shows executable involved)
-o (shows process ID)
-n (numeric addresses)
You can combine them, e.g., netstat -abon, for detailed info.

## File and Disk Management
cd — Show or change directory. Running cd alone shows current directory.

dir — Lists directory contents.
dir /a shows hidden/system files
dir /s lists all files in subfolders recursively

tree — Displays visual directory structure.

mkdir <foldername> — Creates a folder.

rmdir <foldername> — Deletes a folder.

## Viewing and managing files
type <filename> — Displays file content (good for small files).

more <filename> — Displays file content page by page.

copy <source> <destination> — Copies files.

move <source> <destination> — Moves files.

del <filename> or erase <filename> — Deletes files.

Example using wildcard:
copy *.md c:\Markdown — copies all markdown files to that folder.

Handling Permissions Issues
If a file can’t be read due to permissions, moving it may not fix the problem.

Grant yourself read permission with:
icacls "%USERPROFILE%\Desktop\flag.txt" /grant %USERNAME%:R

Then read the file by running:
type "%USERPROFILE%\Desktop\flag.txt"

## Task and Process Management
tasklist — Lists running processes.

tasklist /FI "IMAGENAME eq sshd.exe" — Filters processes by name.

taskkill /PID <PID> — Kills process by its PID.
Example:
taskkill /PID 4567
