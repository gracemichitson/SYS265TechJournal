# SYS265TechJournal

#Lab00
Overview: Configure Ad01, FW01, MGMT01 and WKS01.

FW01:
LAN IP: 10.0.5.2/24
WAN Upstream Gateway: 10.0.17.2
WAN IP: 10.0.17.104
Realitivly easy, Just ike last term, set up the LAN and WAN through the command prompt gui. Make sure that you are able to ping google.com when done with configuration.

WK01:
IP: 10.0.5.100 255.255.255.0
DNS: 10.0.5.2- You will change this to 10.0.5.5 once you want to add the computer to the domain 'grace.local.' and once ad01 is configured.
Navigate to https://10.0.5.2, to configure the firewall. 
Primary DNS Server for Firewall: 8.8.8.8

Ad01: Active Directory
IP: 10.0.5.5
Gateway: 10.0.5.2
DNS;10.0.5.2
It is important to remember that I used the sconfig gui to complete these steps. 
To Install Active Directory on AD01:
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Then install the forrest:
Install-ADDSForest -DOmainName grace.local

Once this step is done, you can now add everything to your domain.

MGMT:
IP: 10.0.5.10
Gateway: 10.0.5.2
DNS: 10.0.5.5

Loging into the domain consists of taking you administrator credentials that where used to set up AD01, and logging into MGMT as administrator@grace.  From there, you can add the features needed, as well as the users needed from your domain.

The lab also consisted of creating a reverse lookup zone for the 10.0.5. network through the Server Manager. Then creating A and PTR records for fw01, mgmt01, wks01, and ad01.

TO query active directory: Get-ADComputer -FIlter *
To enumerate two named domain users: Get-ADUser -filter 'Name -like "grac*"' -Properties MemberOf
Print DNS Server Address and DNS A Records: Get-DNSClientServer Address
Get-DNSServerResourceRecord -ZoneName grace.local -ComputerName ad01-grace -RRType A
