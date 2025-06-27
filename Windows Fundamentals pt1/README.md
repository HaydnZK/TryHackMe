# Windows Fundamentals Part 1 - Notes

This section covers foundational components of the Windows operating system, focusing on editions, the graphical interface, file systems, user permissions, and core system tools.

## 1. Windows Editions

Explored various Windows editions released over time.

Notable feature distinction: BitLocker is available starting with Windows Pro editions.

## 2. Graphical User Interface (GUI)

Examined core interface components:

Desktop

Taskbar

Toolbar

Search bar

Notification Center

These elements form the visual and interactive environment for end users.

## 3. File Systems

Compared legacy and modern file systems:

FAT16/FAT32: Early file systems with size and feature limitations (e.g., 4GB max file size).

HPFS: Older system used mainly on OS/2.

NTFS: Standard modern file system with:

Support for file-level permissions

Compression and encryption

Support for large files

Introduction of Alternate Data Streams (ADS)

## 4. Critical System Folders

%windir%: Environment variable pointing to the Windows installation directory.

System32: Contains essential system files and executables. Critical to OS operation.

Both folders are highly sensitive and should be handled cautiously.

## 5. User Accounts and Permissions

Types of user accounts:

Standard User: Limited privileges

Administrator: Full control over system settings and operations

Explored lusrmgr.msc for managing local users and groups.

## 6. User Account Control (UAC)

UAC prompts for permission or credentials before allowing changes that require administrator-level permission.

Helps protect against malware and unintentional system modifications.

Can be configured to varying levels of strictness for better security.

## 7. Control Panel Overview

Used for both basic and advanced system settings:

Personalization settings like background and themes

Network and Internet settings

Adapter configuration

While some functionality has moved to the Settings app, Control Panel remains relevant.

## 8. Task Manager

Key monitoring tool to track system performance.

Allows viewing and managing:

CPU and GPU usage

Memory and disk utilization

Application-specific resource consumption

Useful for identifying and ending unresponsive programs.

## Summary
This foundational lesson provided an overview of how Windows is structured and operated at a user and system level. Understanding the file system, 
account types, critical folders, and performance tools sets the stage for deeper system administration and security knowledge in later modules.
