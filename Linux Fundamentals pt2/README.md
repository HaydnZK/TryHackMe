# TryHackMe: Linux Fundamentals Part 2 - Notes

## Overview
This room covers several core Linux concepts including using SSH for remote access, working with command-line flags and switches, interacting with the file system, understanding basic file permissions, and reviewing some important Linux directories.

## SSH: Secure Shell Access
SSH (Secure Shell) is a protocol that allows secure communication between devices over a network. It encrypts the data being sent, ensuring confidentiality during transit.

To access a remote machine using SSH, the format is:

ssh tryhackme@<MACHINE_IP>

After entering this command, you're prompted to trust the host and then provide the password for the specified user. Once authenticated, you are connected to the remote machine and can execute commands directly in its terminal.

SSH is primarily used for remote command execution and secure data transmission.

## Flags and Switches
Most Linux commands support optional arguments known as flags or switches. These are typically added using a hyphen and modify the command's behavior.

For example:

ls displays the contents of the working directory

ls -a includes hidden files in the listing, such as .hiddenfolder

To learn more about what flags a command supports:

Use --help after the command

Use man followed by the command to open its manual page

Example: man ls

## Filesystem Interaction
Several common commands are used to interact with files and directories:

touch creates an empty file
Example: touch note

mkdir creates a new directory
Example: mkdir mydirectory

cp copies a file or directory
Example: cp note note2

mv moves or renames files and directories
Example: mv note2 note3

rm deletes files
Example: rm note

rm -R deletes directories and their contents recursively
Example: rm -R mydirectory

file determines the type of a file
Example: file note

## Permissions
Linux files and directories have permissions that control who can read, write, or execute them. Permissions are typically viewed using:

ls -l

Example output: -rw-r--r--

This string can be broken down as follows:

First character: type (dash indicates a regular file)

Next three: owner's permissions

Next three: group's permissions

Final three: others' permissions

Users can switch to a different account using the su command:

su <username> switches to the specified user

su -l <username> switches to the user and starts a full login shell, including their environment and home directory

Without the -l switch, you stay in the current user's environment.

## Common Directories
/etc contains important configuration files for the system, such as the sudoers file

/var is used for data that is frequently modified, such as logs found in /var/log

/root is the home directory for the root user

/tmp is a temporary directory where any user can write files; its contents are typically wiped on reboot

For penetration testers, /tmp can be a useful location to upload or store temporary scripts and tools during a session.
