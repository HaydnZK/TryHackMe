# Windows PowerShell

## Introduction to PowerShell
PowerShell is a task automation framework for Windows. It's object-oriented and scriptable, making it more powerful than traditional CMD. You can launch it from the Start menu or run powershell.exe in CMD.

To confirm you're in PowerShell, check that the prompt starts with PS.

## PowerShell Cmdlets and Syntax
PowerShell uses cmdlets, which follow a verb-noun naming convention.

Examples:

- Get-Help shows help information

- Get-Command lists available commands

- Get-Service lists services

- Start-Service and Stop-Service control services

Use -Name to specify a target, like Get-Service -Name wuauserv.

Use | (pipe) to chain commands. For example:

Get-Service | Where-Object {$_.Status -eq "Running"}

This lists all running services.

## Useful Cmdlets
- Get-Process lists running processes

- Stop-Process -Name notepad ends a process

- Get-EventLog -LogName System -Newest 10 shows the last 10 system log entries

- Get-NetTCPConnection displays current TCP connections

- Test-Connection <host> works like ping

## Working with Files and Directories
PowerShell aliases some commands from CMD for ease of use:

- cd, ls, dir, and pwd are all valid in PowerShell

- Get-ChildItem is the full command behind ls

- New-Item creates files or directories

- Remove-Item deletes them

You can create a directory like this:

New-Item -Path "C:\Temp\Logs" -ItemType Directory

To create a new file:

New-Item -Path "C:\Temp\Logs\info.txt" -ItemType File

## Variables and Objects
Variables in PowerShell start with $. Example:

$myVar = "Hello, PowerShell"

PowerShell treats data as objects. You can access properties and methods with dot notation:

(Get-Process -Name notepad).Id

You can store results in variables and manipulate them further.

## Scripting Basics
PowerShell scripts are .ps1 files. To run one, navigate to the folder and use:

.\script.ps1

Script execution is restricted by default. Check policy with:

Get-ExecutionPolicy

To allow scripts to run:

Set-ExecutionPolicy RemoteSigned

You may need admin rights for this.

## System Administration
You can manage local users with PowerShell:

- Get-LocalUser lists users

- Enable-LocalUser and Disable-LocalUser modify accounts

- New-LocalUser creates new ones

- Set-LocalUser modifies properties like passwords

### User group management:

- Get-LocalGroup

- Add-LocalGroupMember

- Remove-LocalGroupMember

### Service management (again):

- Get-Service

- Start-Service

- Stop-Service

- Restart-Service

## Networking and Firewall
PowerShell offers control over network settings:

- Get-NetIPAddress shows IP info

- New-NetIPAddress sets a new IP address

- Test-NetConnection checks connectivity and port status

### Firewall rules:

- Get-NetFirewallRule

- Enable-NetFirewallRule

- Disable-NetFirewallRule

- New-NetFirewallRule

Example: Allow inbound HTTP traffic

New-NetFirewallRule -DisplayName "Allow HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow

## Conclusion
PowerShell is a powerful tool for Windows administration. It combines scripting, object handling, and automation in a flexible way. Mastering it can significantly increase your efficiency as a Windows user or system administrator.
