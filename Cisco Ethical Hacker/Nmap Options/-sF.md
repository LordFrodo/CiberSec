There are times when a SYN scan might be picked up by a network filter or firewall. In such a case, you need to employ a different type of packet in a port scan. With the TCP FIN scan, a FIN packet is sent to a target port. If the port is actually closed, the target system sends back an RST packet. If nothing is received from the target port, you can consider the port open because the normal behavior would be to ignore the FIN packet. Table 3-5 shows the TCP FIN scan responses.

**NOTE** A TCP FIN scan is not useful when scanning Windows-based systems, as they respond with RST packets, regardless of the port state.