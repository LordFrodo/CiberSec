Enter the **sudo tcpdump** command as shown. Replace the **<_interface_>** text with the interface name that you copied in the previous step. This command requires root user access, so enter **kali** as the password if prompted.

┌──(kali㉿Kali)-[~]

└─$ **sudo tcpdump -i eth0 -s 0 -w packetdump.pcap**

The **-i** command option allows you to specify the interface. If not specified, the tcpdump will capture all traffic on all interfaces.

The **-s** command option specifies the length of the snapshot for each packet. Setting this option to 0 sets it to the default of 262144.

The **-w** command option is used to write the result of the **tcpdump** command to a file. Adding the extension **.pcap** ensures that operating systems and applications will be able to read the file. All recorded traffic will be printed to the file **packetdump.pcap** in the home directory of the user.