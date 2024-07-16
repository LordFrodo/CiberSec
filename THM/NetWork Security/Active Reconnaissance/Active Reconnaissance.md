In the first room of the Network Security Module, we focused on [passive reconnaissance](https://tryhackme.com/jr/passiverecon). In this second room, we focus on active reconnaissance and the essential tools related to it. We learn to use a web browser to collect more information about our target. Moreover, we discuss using simple tools such as [[ping]], [[traceroute]], [[telnet]], and [[nc]] to gather information about the network, system, and services.


In this room, we have covered many various tools. It is easy to put a few of them together via a shell script to build a primitive network and system scanner. You can use `traceroute` to map the path to the target, `ping` to check if the target system responds to ICMP Echo, and `telnet` to check which ports are open and reachable by attempting to connect to them. Available scanners do this at much more advanced and sophisticated levels, as we will see in the next four rooms with [[Nmap]].

|Command|Example|
|---|---|
|ping|`ping -c 10 10.10.126.229` on Linux or macOS|
|ping|`ping -n 10 10.10.126.229` on MS Windows|
|traceroute|`traceroute 10.10.126.229` on Linux or macOS|
|tracert|`tracert 10.10.126.229` on MS Windows|
|telnet|`telnet 10.10.126.229 PORT_NUMBER`|
|netcat as client|`nc 10.10.126.229 PORT_NUMBER`|
|netcat as server|`nc -lvnp PORT_NUMBER`|

Although these are fundamental tools, they are readily available on most systems. In particular, a web browser is installed on practically every computer and smartphone and can be an essential tool in your arsenal for conducting reconnaissance without raising alarms. If you want to gain more profound knowledge of the Developer Tools, we recommend joining [Walking An Application](https://tryhackme.com/room/walkinganapplication).

|Operating System|Developer Tools Shortcut|
|---|---|
|Linux or MS Windows|`Ctrl+Shift+I`|
|macOS|`Option + Command + I`|