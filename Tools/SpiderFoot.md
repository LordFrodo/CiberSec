SpiderFoot is an automated OSINT scanner. It is included with Kali. SpiderFoot queries over 1000 open-information sources and presents the results in an easy-to-use GUI. SpiderFoot can also be run from a console. SpiderFoot seeds its scan with one of the following:

- Domain names
- IP addresses
- Subnet addresses
- Autonomous System Numbers (ASN)
- Email addresses
- Phone numbers
- Personal names

SpiderFoot offers the option of choosing scans based on use case, required data, and by SpiderFoot module. The use cases are:

- All – Get every possible piece of information about the target. This use case can take a very long time to complete.
- Footprint – Understand the target’s network perimeter, associated identities and other information that is yielded by extensive web crawling and search engine use.
- Investigate – This is or targets that you suspect of malicious behavior. Footprinting, blacklist lookups, and other sources that report on malicious sites will be returned.
- Passive – This type of scan is used if it is undesirable for the target to suspect that it is being scanned. This is a form of passive OSINT.

In a terminal, enter the following command:

┌──(kali㉿Kali)-[~]

└─$ **spiderfoot -l 127.0.0.1:5001**

The command should run without errors. Open a browser and enter the IP address and port for the SpiderFoot GUI. You will see the SpiderFoot interface appear. If this is the first time that SpiderFoot has been opened in this VM, you will see the Scans screen. This screen displays a list of all the scans recently run. In this example it is empty.