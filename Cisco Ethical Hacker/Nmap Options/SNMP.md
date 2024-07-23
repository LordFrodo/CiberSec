Simple Network Management Protocol (SNMP) is a protocol that many individuals and organizations use to manage network devices. SNMP uses UDP port 161. In SNMP implementations, every network device contains an SNMP agent that connects with an independent SNMP server (also known as the SNMP manager). An administrator can use SNMP to obtain health information and the configuration of a networking device, to change the configuration and to perform other administrative tasks. As you can imagine, this is very attractive to attackers because they can leverage SNMP vulnerabilities to perform similar actions in a malicious way.

There are several versions of SNMP. The two most popular versions today are SNMPv2c and SNMPv3. SNMPv2c uses community strings, which are passwords that are applied to a networking device to allow an administrator to restrict access to the device in two ways: by providing read-only or read/write access.

The managed device information is kept in a database called the Management Information Base (MIB).

A common SNMP attack involves an attacker enumerating SNMP services and then checking for configured default SNMP passwords. Unfortunately, this is one of the major flaws of many implementations because many users leave weak or default SNMP credentials in networking devices. SNMPv3 uses usernames and passwords and it is more secure than all previous SNMP versions. Attackers can still perform dictionary and brute-force attacks against SNMPv3 implementations, however. A more modern and security implementation involves using NETCONF with newer infrastructure devices (such as routers and switches).

In Module 3, you learned how to use the Nmap scanner. You can leverage Nmap Scripting Engine (NSE) scripts to gather information from SNMP-enabled devices and to brute-force weak credentials. In Kali Linux, the NSE scripts are located at /usr/share/nmap/scripts by default.

Example 5-5 shows the available SNMP-related NSE scripts in a Kali Linux system.

```
root@kali:/usr/share/nmap/scripts# ls -1 snmp*snmp-brute.nsesnmp-hh3c-logins.nsesnmp-info.nsesnmp-interfaces.nsesnmp-ios-config.nsesnmp-netstat.nsesnmp-processes.nsesnmp-sysdescr.nsesnmp-win32-services.nsesnmp-win32-shares.nsesnmp-win32-software.nsesnmp-win32-users.nseroot@kali:/usr/share/nmap/scripts#
```

In addition to NSE scripts, you can use the **snmp-check** tool to perform an _SNMP walk_ in order to gather information on devices configured for SNMP.