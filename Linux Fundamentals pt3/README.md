# Linux Fundamentals pt3
## Terminal Text Editors
This section explored terminal-based text editors, specifically nano and vim.

- nano <filename> creates a new file or opens an existing one for editing. It is simple to use and displays shortcuts at the bottom of the screen, such as searching text, copying, jumping to a line, and more.

- vim is more advanced and highly customizable. It supports features like syntax highlighting and works across all terminals, even when nano is not installed. Vim is especially useful for writing or editing code. There are tutorials and a dedicated TryHackMe room available for learning vim.

## General and Useful Utilities
### File Transfers
wget <URL> downloads files from the internet over HTTP. Example:

wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt

scp allows secure file transfers between systems over SSH. Example:

scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt

This uploads a file from the local system to a remote system.

scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt

This downloads a file from a remote system to the local system.

### Simple Web Server with Python
Ubuntu machines come with Python3 installed, which includes a lightweight HTTP server module.

To serve files:

python3 -m http.server

This serves files from the current directory on port 8000.

From another system, files can be downloaded using wget:

wget http://MACHINE_IP:8000/myfile

This only works if the exact file name is known. There is no file indexing. For more advanced file sharing, tools like Updog can be used, though not covered here.

## Processes 101
Processes are programs that run on the machine and are managed by the kernel. Each has a Process ID (PID).

- ps displays the user’s current running processes

- ps aux shows all processes on the system

- top displays system resource usage and running processes in real time

### Signals
Processes can be managed using signals. The kill command followed by a PID terminates a process.

Common signals include:

- SIGTERM: Allows the process to exit gracefully

- SIGKILL: Forces the process to terminate immediately

- SIGSTOP: Suspends the process

### Namespaces and systemd
Namespaces isolate process resources like CPU and memory. The first process to run on system boot has a PID of 0. On Ubuntu, this is init, now commonly replaced by systemd, which manages system services and user processes.

Services can be configured to start automatically at boot using systemctl. The basic syntax is:

systemctl <option> <service>

Options include:

- start

- stop

- enable

- disable

Example: systemctl start apache2

### Foreground and Background Processes
Processes run in either the foreground or background.

Running a command with & puts it in the background

Using ctrl + z suspends a running process

fg brings a background process to the foreground

This allows multitasking within the terminal, such as running long operations in the background while continuing other tasks.

## Maintaining Your System: Automation
The cron service allows scheduled task automation using crontabs.

A crontab entry follows this format:

- MIN: What minute to execute at
- HOUR: What hour to execute at
- DOM: What day of the month to execute at
- MON: What month of the year to execute at
- DOW: What day of the week to execute at
- CMD: The actual command that will be executed

Each line defines when and how a command should run.

Example: run a backup every 12 hours

0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/

Edit crontabs with:

crontab -e

## Maintaining Your System: Package Management
Linux systems use package managers like apt to install and manage software.

- Developers submit software to repositories, which are managed and reviewed

- Repositories can be added with add-apt-repository or manually

Installing software involves:

1. Adding the developer’s GPG key:

wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

2. Creating a source list file:

cd /etc/apt/sources.list.d
touch sublime-text.list
nano sublime-text.list
(Add the line: deb https://download.sublimetext.com/ apt/stable/)

3. Updating apt:

apt update

4. Installing the software:

apt install sublime-text

To remove:

- Remove the repository with add-apt-repository --remove or delete the file manually

- Remove the software with:

apt remove sublime-text

## Maintaining Your System: Logs
Logs are typically stored in /var/log. These contain data about system and service activity.

Examples include:

- Apache2 web server logs

- Fail2ban logs (used to detect brute-force attempts)

- UFW logs (firewall activity)

Logs are rotated automatically by the OS to manage file size and system performance. Logs provide essential insight for system monitoring, troubleshooting, and security investigations.
