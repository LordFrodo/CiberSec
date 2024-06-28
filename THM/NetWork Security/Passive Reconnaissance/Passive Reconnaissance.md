In this room, after we define passive reconnaissance and active reconnaissance, we focus on essential tools related to passive reconnaissance. We will learn three command-line tools:

- [[whois]] to query WHOIS servers
- [[nslookup]] to query [[DNS]] servers
- [[dig]] to query [[DNS]] servers

We use `whois` to query WHOIS records, while we use `nslookup` and `dig` to query DNS database records. These are all publicly available records and hence do not alert the target.

We will also learn the usage of two online services:

- [[DNSDumpster]]
- [[Shodan.io]]

These two online services allow us to collect information about our target without directly connecting to it.

Pre-requisites: This room requires basic networking knowledge along with basic familiarity with the command line. The modules [Network Fundamentals](https://tryhackme.com/module/network-fundamentals) and [Linux Fundamentals](https://tryhackme.com/module/linux-fundamentals) provide the required knowledge if necessary.

In this room, we focused on passive reconnaissance. In particular, we covered command-line tools, `whois`, `nslookup`, and `dig`. We also discussed two publicly available services [DNSDumpster](https://dnsdumpster.com/) and [Shodan.io](https://www.shodan.io/). The power of such tools is that you can collect information about your targets without directly connecting to them. Moreover, the trove of information you may find using such tools can be massive once you master the search options and get used to reading the results.

| Purpose                             | Commandline Example                       |
| ----------------------------------- | ----------------------------------------- |
| Lookup WHOIS record                 | `whois tryhackme.com`                     |
| Lookup DNS A records                | `nslookup -type=A tryhackme.com`          |
| Lookup DNS MX records at DNS server | `nslookup -type=MX tryhackme.com 1.1.1.1` |
| Lookup DNS TXT records              | `nslookup -type=TXT tryhackme.com`        |
| Lookup DNS A records                | `dig tryhackme.com A`                     |
| Lookup DNS MX records at DNS server | `dig @1.1.1.1 tryhackme.com MX`           |
| Lookup DNS TXT records              | `dig tryhackme.com TXT`                   |
