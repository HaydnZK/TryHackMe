## Managing Users and Delegating Control

# Task 1: Removing an Unnecessary OU

To start, I needed to clean up an unwanted organizational unit in Active Directory. I compared the list of THM OUs with the organizational chart and noticed that the Research and Development OU wasn’t supposed to be there.

I couldn’t delete it normally, so I did the following:

In Active Directory Users and Computers, I went to the View menu and enabled Advanced Features.

I right-clicked the Research and Development OU and opened Properties.

Under the Object tab, I unchecked "Protect object from accidental deletion."

After that, I was able to delete the OU.

# Task 2: Logging into Sophie's Desktop

I needed to RDP into Sophie’s account to retrieve a flag from her desktop. To do this, I had to give Phillip permission to reset her password.

# Delegating Control

In Active Directory, I right-clicked the Sales OU and selected Delegate Control.

I added Phillip using the Check Names button to confirm the account.

I granted him permission to reset user passwords and force password changes at next login.

# Getting the Computer Name

Before connecting via RDP, I used the following command in PowerShell to find the NetBIOS name: hostname

# Resetting Sophie's Password

Once logged in as Phillip via RDP, I opened PowerShell and ran:

Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose

It prompted me for a new password and confirmed the operation with a verbose message indicating success.

Next, I forced Sophie to change her password at login:

Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose

Logging Off Phillip to Free the RDP Session

Since the system only allows one RDP session at a time, I had to log off Phillip’s session to continue.

I ran this command to list active sessions: query session

It returned the following:

SESSIONNAME USERNAME ID STATE
rdp-tcp#2 Administrator 2 Active
rdp-tcp#4 PHILLIP 3 Active

Then I logged off Phillip with: logoff 3

Logging in as Sophie

After that, I opened RDP again and logged in using Sophie’s account and the new password. I was prompted to change her password as expected. 

Once logged in, I was able to access her desktop and retrieve the flag file.

## Organizing Devices in Active Directory

We noticed that the default Computers OU in Active Directory contained a mix of laptops, desktops, and servers. To improve organization and 
reflect a more logical structure, we created two new Organizational Units:

- Workstations

- Servers

To do this, we right-clicked on the domain name at the top of the AD tree and selected New > Organizational Unit to create each folder.

Once the OUs were created, we sorted the devices as follows:

- All laptops and desktop computers were moved into the Workstations OU.

- All servers were moved into the Servers OU.

After moving the devices, we verified that there were a total of 7 workstations in the Workstations OU.

## Group Policy Management

Reviewing Existing GPOs
We started by opening Group Policy Management and locating the Group Policy Objects folder. The following GPOs were present:

Default Domain Controllers Policy

Default Domain Policy

RDP Policy

Default Domain Policy and RDP Policy were both linked to thm.local.
Default Domain Controllers Policy was linked to the Domain Controllers OU.

In the Settings tab of the Default Domain Policy, we saw that it only applies to Computer Configuration, though GPOs can include both user and computer settings. The Security Filtering was set to Authenticated Users, which means it applies broadly across the domain.

Expanding Computer Configuration > Policies > Windows Settings > Security Settings revealed various default configurations, including:

Password requirements

Account lockout rules

Encryption policies

Editing Default Password Requirements
To change the Minimum Password Length from 7 to 10 characters:

Right-click the Default Domain Policy and select Edit

Navigate to:
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy

Double-click Minimum password length and set it to 10

Apply and close

Double-clicking any setting also provides an explanation of its purpose.

SYSVOL and GPO Distribution
Group Policy settings are stored and distributed using the SYSVOL share on the Domain Controller:

C:\Windows\SYSVOL\sysvol\

Domain-joined computers automatically check for GPO updates every 90 to 120 minutes. You can force an update manually using:

gpupdate /force

Creating and Applying New GPOs
We created two new GPOs to apply targeted settings.

1. Restricting Control Panel Access for Non-IT Users
To prevent access to the Control Panel and PC settings for users outside of the IT department:

Create a new GPO

Edit the policy and navigate to:
User Configuration > Administrative Templates > Control Panel

Enable:
Prohibit access to Control Panel and PC settings

Link the GPO to the following OUs:

Marketing

Management

Sales

2. Enforcing Screen Lock After Inactivity
To configure all computers to automatically lock after 5 minutes of inactivity:

Create a new GPO named Screen Lockout Time

Edit the policy and navigate to:
Computer Configuration > Policies > Administrative Templates > Control Panel > Personalization

Enable and configure:

Screen saver timeout: 300 seconds

Password protect the screen saver

Link the GPO to the root of the domain so it applies to all computers

## Authentication Methods
Within Windows, all credentials are stored in the Domain Controllers. In order to authenticate using domain credentials, the Domain Controller must verify 
if the credentials are correct. This is done using one of two protocols:

Kerberos: Used by recent versions of Windows and is the default protocol in modern domains.

NetNTLM: The legacy version, still kept for compatibility.

# Kerberos Authentication Steps
The user sends their username and a timestamp encrypted with a key derived from their password to the KDC (Key Distribution Center), which is usually hosted 
on the Domain Controller. The KDC is responsible for issuing Kerberos tickets.

The KDC replies with a TGT (Ticket Granting Ticket) that allows the user to request tickets for specific services. This avoids sending credentials every time 
a service is accessed. Along with the TGT, the user receives a Session Key, used to generate future requests.

When the user wants to connect to a service (e.g., a file share, website, or database), they request a TGS (Ticket Granting Service). This request includes:

Their username and a timestamp encrypted with the Session Key

The TGT

The SPN (Service Principal Name), which identifies the specific service

The KDC sends back a TGS and a Service Session Key. The TGS is encrypted with a key derived from the service's account password hash. The TGS contains a copy of the Service Session Key so the service can decrypt it and authenticate the session.

The user then sends the TGS to the desired service. The service decrypts the ticket using its password hash, validates the Service Session Key, and grants access.

# NetNTLM Authentication Steps
The client sends an authentication request to the server they wish to access.

The server generates a random number and sends it to the client as a challenge.

The client uses the NTLM password hash, the challenge, and additional known values to generate a response and sends it back.

The server forwards the challenge and response to the Domain Controller.

The Domain Controller uses the challenge to recalculate the expected response and compares it to the client’s version. If they match, the user is authenticated.

The server then sends the authentication result back to the client.

## Trees, Forests, and Trusts
A single domain is suitable for smaller networks, but as an organization grows, it may need to scale to include multiple domains.

# Trees
When a company expands to other regions (like new countries), different policies and legal requirements might apply. New IT teams in those regions need the ability to manage their local resources without interfering with others.

Active Directory supports this through multiple domains. When these domains share the same namespace (e.g., thm.local), they can be joined into a tree.

Example structure:

Root Domain: thm.local

Subdomains: uk.thm.local, us.thm.local

Each domain manages its own users, computers, and GPOs. IT in the UK controls its domain controller, and the US has its own as well. This structure gives Domain Admins in each region control over their own environments, while keeping them isolated from others.

An additional group, Enterprise Admins, is introduced at this level. Members of this group have administrative rights over all domains in the enterprise. Each domain still maintains its own Domain Admins group for local control.

# Forests
When different domain trees exist under separate namespaces (e.g., thm.local and mht.local), they form a forest. This may happen when a company acquires another organization with its own IT infrastructure.

In this example:

Tree 1: thm.local, uk.thm.local, us.thm.local

Tree 2: mht.local

These trees form a forest, which allows for management across the larger organization, while keeping trees logically separated.

# Trust Relationships
Trusts allow users in one domain to access resources in another. Trusts can be:

One-way: If Domain A trusts Domain B, users from Domain B can access Domain A's resources, but not the other way around.

Two-way: Both domains trust each other and can authorize users reciprocally.

Two-way trusts are typically established by default when domains are part of the same tree or forest.

Note: A trust relationship enables the possibility of access, but authorization still needs to be granted manually. A trust doesn't mean users can access everything by default.
