# Windows Fundamentals Part 2 - Notes

This lesson focused on key tools and components within the Windows operating system that are critical for troubleshooting, configuration, and system management.

## 1. System Configuration (msconfig)

Purpose: Used for troubleshooting and diagnosing startup issues.

Access: Can be run by typing msconfig in the Start menu or Run prompt.

Tabs:

General: Allows users to choose which devices and services load at startup (Normal, Diagnostic, or Selective startup).

Boot: Contains options for how the OS boots, such as Safe Boot, No GUI Boot, etc.

Startup: In modern Windows versions, this is redirected to Task Manager, where startup applications are managed.

Services: Displays all system services, whether currently running or not. Users can enable/disable services.

Tools: Lists various built-in Windows tools with descriptions and a launch button for each.

UAC Configuration: From msconfig or the Control Panel, users can access a slider to configure UAC settings, from "Always notify" to "Never notify."

## 2. Computer Management (compmgmt.msc)
A management console containing several administrative tools. It has three main sections:

System Tools:

Task Scheduler: Automates tasks to run at specific times or under certain conditions.

Event Viewer: Allows users to view logs and audit trails. Types of events include:

Error

Warning

Information

Success Audit

Failure Audit

Shared Folders: View open files, sessions, and shared resources.

Performance: Legacy tool for viewing system performance metrics.

Device Manager: Manage hardware and drivers.

Storage:

Disk Management: Used to manage partitions and volumes. Tasks include:

Set up a new drive

Extend/shrink partitions

Assign/change drive letters

Services and Applications:

Services: Allows in-depth configuration of services, including properties and dependencies.

WMI Control: Windows Management Instrumentation, used for managing the system through scripting or remote access. Superseded by PowerShell in many cases.

## 3. System Information Tool (msinfo32)

Provides a detailed view of the system's hardware, components, and software environment.

Sections:

Hardware Resources: Includes I/O, IRQs, DMA, memory, and other technical specs (mainly for advanced users).

Components: Displays information about internal devices. In the VM, display and input devices were viewable.

Software Environment: Lists drivers, running tasks, environment variables, network connections, and more.

Environment Variables: Includes paths, processor count, temporary folder locations, and system-wide values.

## 4. Resource Monitor (resmon)

Real-time system monitoring tool.

Tracks usage for CPU, memory, disk, and network.

Allows filtering by processes.

Can pause, start, and stop services.

Includes process analysis, allowing users to resolve issues without fully terminating applications.

Overview tab shows:

CPU usage

Disk activity

Network usage

Memory usage

## 5. Command Prompt (cmd.exe)

Original interface for interacting with Windows systems.

Commands covered:

hostname: Shows the device name.

whoami: Displays current logged-in user.

ipconfig: Shows network interface settings.

netstat: Displays TCP/IP connections and protocol stats.

net: Manages network resources.

Useful command options:

-a, -b, -e: Add functionality to basic commands like netstat.

help, /?: Display command usage and syntax.

## 6. Windows Registry

A hierarchical database that stores configuration data.

Contains settings for:

User profiles

Application associations

Folder and icon properties

Hardware settings

Port configurations

Editing the registry can break systems if done improperly, so caution is always recommended.

## Summary
This session focused on powerful tools within Windows that support monitoring, diagnosing, and configuring the system. Whether it’s viewing 
hardware info through msinfo32, managing services in compmgmt.msc, or digging into performance issues with resmon, these utilities form the core of effective Windows administration.
