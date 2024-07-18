Ping should remind you of the game ping-pong (table tennis). You throw the ball and expect to get it back. The primary purpose of ping is to check whether you can reach the remote system and that the remote system can reach you back. In other words, initially, this was used to check network connectivity; however, we are more interested in its different uses: checking whether the remote system is online.

In simple terms, the ping command sends a packet to a remote system, and the remote system replies. This way, you can conclude that the remote system is online and that the network is working between the two systems.

If you prefer a pickier definition, the ping is a command that sends an ICMP Echo packet to a remote system. If the remote system is online, and the ping packet was correctly routed and not blocked by any firewall, the remote system should send back an ICMP Echo Reply. Similarly, the ping reply should reach the first system if appropriately routed and not blocked by any firewall.

The objective of such a command is to ensure that the target system is online before we spend time carrying out more detailed scans to discover the running operating system and services.

On your AttackBox terminal, you can start to use ping as `ping MACHINE_IP` or `ping HOSTNAME`. In the latter, the system needs to resolve HOSTNAME to an IP address before sending the ping packet. If you don’t specify the count on a Linux system, you will need to hit `CTRL+c` to force it to stop. Hence, you might consider `ping -c 10 MACHINE_IP` if you just want to send ten packets. This is equivalent to `ping -n 10 MACHINE_IP` on a MS Windows system.

Technically speaking, ping falls under the protocol ICMP (Internet Control Message Protocol). ICMP supports many types of queries, but, in particular, we are interested in ping (ICMP echo/type 8) and ping reply (ICMP echo reply/type 0). Getting into ICMP details is not required to use ping.

In the following example, we have specified the total count of packets to 5. From the AttackBox’s terminal, we started pinging `MACHINE_IP`. We learned that `MACHINE_IP` is up and is not blocking ICMP echo requests. Moreover, any firewalls and routers on the packet route are not blocking ICMP echo requests either.

AttackBox Terminal

           `user@AttackBox$ ping -c 5 MACHINE_IP PING MACHINE_IP (MACHINE_IP) 56(84) bytes of data. 64 bytes from MACHINE_IP: icmp_seq=1 ttl=64 time=0.636 ms 64 bytes from MACHINE_IP: icmp_seq=2 ttl=64 time=0.483 ms 64 bytes from MACHINE_IP: icmp_seq=3 ttl=64 time=0.396 ms 64 bytes from MACHINE_IP: icmp_seq=4 ttl=64 time=0.416 ms 64 bytes from MACHINE_IP: icmp_seq=5 ttl=64 time=0.445 ms  --- MACHINE_IP ping statistics --- 5 packets transmitted, 5 received, 0% packet loss, time 4097ms rtt min/avg/max/mdev = 0.396/0.475/0.636/0.086 ms`
        

In the example above, we saw clearly that the target system is responding. The ping output is an indicator that it is online and reachable. We have transmitted five packets, and we received five replies. We notice that, on average, it took 0.475 ms (millisecond) for the reply to reach our system, with the maximum being 0.636 ms.  

From a penetration testing point of view, we will try to discover more about this target. We will try to learn as much as possible, for example, which ports are open and which services are running.

Let’s consider the following case: we shut down the target virtual machine and then tried to ping `MACHINE_IP`. As you would expect in the following example, we don’t receive any reply.

AttackBox Terminal

           `user@AttackBox$ ping -c 5 MACHINE_IP PING MACHINE_IP (MACHINE_IP) 56(84) bytes of data. From ATTACKBOX_IP icmp_seq=1 Destination Host Unreachable From ATTACKBOX_IP icmp_seq=2 Destination Host Unreachable From ATTACKBOX_IP icmp_seq=3 Destination Host Unreachable From ATTACKBOX_IP icmp_seq=4 Destination Host Unreachable From ATTACKBOX_IP icmp_seq=5 Destination Host Unreachable  --- MACHINE_IP ping statistics --- 5 packets transmitted, 0 received, +5 errors, 100% packet loss, time 4098ms pipe 4`
        

In this case, we already know that we have shut down the target computer that has MACHINE_IP. For each ping, the system we are using, AttackBox in this case, is responding with “Destination Host Unreachable.” We can see that we have transmitted five packets, but none was received, resulting in a 100% packet loss.  

Generally speaking, when we don’t get a ping reply back, there are a few explanations that would explain why we didn’t get a ping reply, for example:

- The destination computer is not responsive; possibly still booting up or turned off, or the OS has crashed.
- It is unplugged from the network, or there is a faulty network device across the path.
- A firewall is configured to block such packets. The firewall might be a piece of software running on the system itself or a separate network appliance. Note that MS Windows firewall blocks ping by default.
- Your system is unplugged from the network.