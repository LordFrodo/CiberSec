Find the IP address of a domain name using `nslookup`, which stands for Name Server Look Up. You need to issue the command `nslookup DOMAIN_NAME`, for example, `nslookup tryhackme.com`. Or, more generally, you can use `nslookup OPTIONS DOMAIN_NAME SERVER`. These three main parameters are:

- OPTIONS contains the query type as shown in the table below. For instance, you can use `A` for IPv4 addresses and `AAAA` for IPv6 addresses.
- DOMAIN_NAME is the domain name you are looking up.
- SERVER is the DNS server that you want to query. You can choose any local or public DNS server to query. Cloudflare offers `1.1.1.1` and `1.0.0.1`, Google offers `8.8.8.8` and `8.8.4.4`, and Quad9 offers `9.9.9.9` and `149.112.112.112`. There are many [more public DNS servers](https://duckduckgo.com/?q=public+dns) that you can choose from if you want alternatives to your ISP’s DNS servers.

|Query type|Result|
|---|---|
|A|IPv4 Addresses|
|AAAA|IPv6 Addresses|
|CNAME|Canonical Name|
|MX|Mail Servers|
|SOA|Start of Authority|
|TXT|TXT Records|

For instance, `nslookup -type=A tryhackme.com 1.1.1.1` (or `nslookup -type=a tryhackme.com 1.1.1.1` as it is case-insensitive) can be used to return all the IPv4 addresses used by tryhackme.com.

![[Pasted image 20240627180408.png]]
The A and AAAA records are used to return IPv4 and IPv6 addresses, respectively. This lookup is helpful to know from a penetration testing perspective. In the example above, we started with one domain name, and we obtained three IPv4 addresses. Each of these IP addresses can be further checked for insecurities, assuming they lie within the scope of the penetration test.

Let’s say you want to learn about the email servers and configurations for a particular domain. You can issue `nslookup -type=MX tryhackme.com`. Here is an example:

![[Pasted image 20240627180422.png]]

We can see that tryhackme.com’s current email configuration uses Google. Since MX is looking up the Mail Exchange servers, we notice that when a mail server tries to deliver email `@tryhackme.com`, it will try to connect to the `aspmx.l.google.com`, which has order 1. If it is busy or unavailable, the mail server will attempt to connect to the next in order mail exchange servers, `alt1.aspmx.l.google.com` or `alt2.aspmx.l.google.com`.

Google provides the listed mail servers; therefore, we should not expect the mail servers to be running a vulnerable server version. However, in other cases, we might find mail servers that are not adequately secured or patched.

Such pieces of information might prove valuable as you continue the passive reconnaissance of your target. You can repeat similar queries for other domain names and try different types, such as `-type=txt`. Who knows what kind of information you might discover along your way!