Example: nmap -sV -Pn http://10.10.82.0/   

Nmap Scan Types

The following sections cover some of the most common Nmap scanning options used for specific scenarios, including the following:

- TCP Connect Scan (**[[-sT]]**)
- TCP SYN Scan ([[-sS]])
- UDP Scan (**[[-sU]]**)
- TCP FIN Scan (**[[-sF]]**)
- Host Discovery Scan (**[[-sn]]**)
- Don't get the DNS server (-n)
- Verbose (-v)
- Debugging (-d)
- Get OS (-O)
- Save the Output of nmap into a file (-oN "fileName")
- Save the Output of nmap into a XML file (-oX "filename")
- Get Traceroute to the target(--traceroute)
- Reason of Nmap conclusions (--reason)
- Fragment IP data (-f)
- Get all possible DNS even offline (-R)
- Scan the 100 most common ports (-F)
- Use a ICMP (ping request) to discover hosts (-PE)
- List of Targets (-sL)
- Only runs a ARP scan ([[-PR]])
- Timing Options (**[[-T 0-5]]**)
- Host Enumeration (**[[-sP]]**) (This is the same as -sn)
- Run Most Common or Default NSE ([[-sC]] or --script=default)
- TCP SYN Ping Scan ([[-PS]])
- TCP ACK Ping Scan ([[-PA]])
- UDP Ping Scan ([[-PU]])
- [[Web Page or Application Enumeration]] & Service Version Scan (**-sV**)
- [[User Enumeration]]
- [[Group Enumeration]]
- [[Network Share Enumeration]]
- [[Service Enumeration]] 
- [[SNMP]]
- [[Simple Mail Transfer Protocol]]
- 