Identifying systems on a network that are sharing files, folders, and printers is helpful in building out an attack surface of an internal network. The Nmap **smb-enum-shares** NSE script uses Microsoft Remote Procedure Call (MSRPC) for **_network share enumeration_**. The syntax of the Nmap **smb-enum-shares.nse** script is as follows:

**nmap --script smb-enum-shares.nse -p 445** _<host>_