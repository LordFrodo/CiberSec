_SMTP_ _open relay_ is the term used for an email server that accepts and _relays_ (that is, sends) emails from any user. It is possible to abuse these configurations to send spoofed emails, spam, phishing, and other email-related scams. Nmap has an NSE script to test for open relay configurations. The details about the script are available at [_https://svn.nmap.org/nmap/scripts/smtp-open-relay.nse_](https://svn.nmap.org/nmap/scripts/smtp-open-relay.nse), and Example 5-6 shows how you can use the script against an email server (10.1.2.14).

**_Example 5-6_** _-_ _SMTP Open Relay NSE Script_

```
root@kali:/usr/share/nmap/scripts# nmap --script smtp-open-relay.nse10.1.2.14Starting Nmap 7.60 ( https://nmap.org ) at 2018-04-15 13:32 EDTNmap scan report for 10.1.2.14Host is up (0.00022s latency).PORT STATE SERVICE25/tcp open smtp|_smtp-open-relay: Server is an open relay (16/16 tests)Nmap done: 1 IP address (1 host up) scanned in 6.82 secondsroot@kali:/usr/share/nmap/scripts# 
```
