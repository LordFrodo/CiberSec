Enum4linux is a tool for enumerating information from Windows and Samba. Samba is an application that enables Linux and Apple clients to participate in Windows networks. It enables non-Windows clients to utilize the Server Message Block (SMB) protocol to access file and print services. Samba servers can participate in a Windows domain, both as a client and a server.

Resume: Its used to get usernames and more in a **local network** by SMB.

One way to identify potential targets for SMB enumeration is to examine the open ports. In an earlier lab, you used Nmap to find and enumerate open ports on target systems. Common open ports on SMB servers are:

TCP 135           RPC

TCP 139           NetBIOS Session

TCP 389           LDAP Server

TCP 445           SMB File Service

TCP 9389          Active Directory Web Services

TCP/UDP 137   NetBIOS Name Service

UDP 138           NetBIOS Datagram

1. Two virtual networks are included in the Kali VM with Docker containers. Use the **nmap -sN** command to find the services available on hosts in the 172.17.0.0 virtual network.

**Use**
└─$ **sudo su**

[sudo] password for kali:

┌──(root㉿kali)-[/home/kali]

└─# **enum4linux**