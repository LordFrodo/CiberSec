When it comes to enumeration via packet crafting and generation, Scapy is one of pentesters' favorite tools and frameworks. Scapy is a very comprehensive Python-based framework or ecosystem for packet generation. This section looks at some of the simple ways you can use this tool to perform basic network reconnaissance.

**NOTE** Scapy must be run with root permissions to be able to modify packets.

Launching the Scapy interactive shell is as easy as typing **sudo scapy** from a terminal window.

Example 3-34 shows how easy it is to begin crafting packets. In this example, a simple ICMP packet is crafted with **malicious_payload** as the payload being sent to the destination host 192.168.88.251.

**_Example 3-34_** _-_ _Crafting a Simple ICMP Packet Using Scapy_
```
>>> send(IP(dst="192.168.88.251")/ICMP()/"malicious_payload").Sent 1 packets.
```

Example 3-35 shows the ICMP packet received by the target system (192.168.88.225/vulnhost-1). The tshark packet capture tool is used to capture the crafted ICMP packet.

**_Example 3-35_** _-_ _Collecting a Crafted Packet by Using tshark_
```
omar@vulnhost-1 ~ % sudo tshark host 192.168.78.142Capturing on 'eth0'     1 0.000000000 192.168.78.142 ? 192.168.88.251 ICMP 60 Echo (ping) request   id=0x0000, seq=0/0, ttl=63     2 0.000026929 192.168.88.251 ? 192.168.78.142 ICMP 59 Echo (ping) reply       id=0x0000, seq=0/0, ttl=64 (request in 1) 
```
Scapy supports a large number of protocols. You can use the **ls()** function to list all available formats and protocols. You can use the **ls()** function to display all the options and fields of a specific protocol or packet format supported by Scapy, as TCP or DNS. 

**Example**
ls(TCP)
ls(DNS)

You can use the **explore()** function to navigate the Scapy layers and protocols. You can use the **explore()** function with any packet format or protocol. Example 3-39 shows the packets contained in scapy.layers.dns using the **explore(“dns”)** function.

You can use Scapy as a scanner in many different ways. Omar Santos has several examples of Python scripts to perform network and system scanning using Scapy at his GitHub repository; see _[https://github.com/The-Art-of-Hacking/h4cker/blob/master/python_ruby_and_bash](https://github.com/The-Art-of-Hacking/h4cker/blob/master/python_ruby_and_bash)_. However, you can do a simple TCP SYN scan to any given port, as demonstrated in Example 3-40. In this example, a TCP port 445 SYN packet is sent to the host with the IP address 192.168.88.251. The output indicates that it received one answer, but it doesn’t specify what the actual answer (response) was.

**_Example 3-40_** _-_ _Sending a TCP SYN Packet Using Scapy_

```
>>> ans, unans = sr(IP(dst='192.168.88.251')/TCP(dport=445,flags='S'))Begin emission:Finished sending 1 packets.....*Received 5 packets, got 1 answers, remaining 0 packets>>>
```

Example 3-41 shows the packet capture on the target host (192.168.88.251).

**_Example 3-41_** _-_ _The Packet Capture of the TCP Packets on the Target Host_

```
omar@vulnhost-1 ~ % sudo tshark host 192.168.78.142Running as user "root" and group "root". This could be dangerous.Capturing on 'eth0'     1 0.000000000 192.168.78.142 ? 192.168.88.251 TCP 60 20 ? 445 [SYN] Seq=0 Win=8192 Len=0     2 0.000033735 192.168.88.251 ? 192.168.78.142 TCP 58 445 ? 20 [SYN, ACK] Seq=0 Ack=1 Win=64240 Len=0 MSS=1460          3 0.001065273 192.168.78.142 ? 192.168.88.251 TCP 60 20 ? 445 [RST] Seq=1 Win=0 Len=0
```