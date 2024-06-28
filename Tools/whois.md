WHOIS is a request and response protocol that follows the [RFC 3912](https://www.ietf.org/rfc/rfc3912.txt) specification. A WHOIS server listens on TCP port 43 for incoming requests. The domain registrar is responsible for maintaining the WHOIS records for the domain names it is leasing. The WHOIS server replies with various information related to the domain requested. Of particular interest, we can learn:

- Registrar: Via which registrar was the domain name registered?
- Contact info of registrant: Name, organization, address, phone, among other things. (unless made hidden via a privacy service)
- Creation, update, and expiration dates: When was the domain name first registered? When was it last updated? And when does it need to be renewed?
- Name Server: Which server to ask to resolve the domain name?

To get this information, we need to use a `whois` client or an online service. Many online services provide `whois` information; however, it is generally faster and more convenient to use your local whois client. Using the AttackBox (or your local Linux machine, such as Parrot or Kali), you can easily access your whois client on the terminal. The syntax is `whois DOMAIN_NAME`, where `DOMAIN_NAME` is the domain about which you are trying to get more information. Consider the following example executing `whois tryhackme.com`.

![[Pasted image 20240627174219.png]]

We can see plenty of information; we will inspect them in the order displayed. First, we notice that we were redirected to `whois.namecheap.com` to get our information. In this case and at the time being, `namecheap.com` is maintaining the WHOIS record for this domain name. Furthermore, we can see the creation date along with the last-update date and expiration date.

Next, we obtain information about the registrar and the registrant. We can find the registrant’s name and contact information unless they are using some privacy service. Although not displayed above, we get the admin and tech contacts for this domain. Finally, we see the domain name servers that we should query if we have any DNS records to look up.

The information collected can be inspected to find new attack surfaces, such as social engineering or technical attacks. For instance, depending on the scope of the penetration test, you might consider an attack against the email server of the admin user or the DNS servers, assuming they are owned by your client and fall within the scope of the penetration test.

It is important to note that due to automated tools abusing WHOIS queries to harvest email addresses, many WHOIS services take measures against this. They might redact email addresses, for instance. Moreover, many registrants subscribe to privacy services to avoid their email addresses being harvested by spammers and keep their information private.