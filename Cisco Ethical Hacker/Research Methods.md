Most of us use search engines such as DuckDuckGo, Bing, and Google to locate information. What you might not know is that search engines, such as Google, can perform much more powerful searches than most people ever dream of. Google can translate documents, perform news searches, and do image searches. In addition, hackers and attackers can use it to do something that has been termed _Google hacking_.

By using basic search techniques combined with advanced operators, both you and attackers can use Google as a powerful vulnerability search tool. The following are some advanced operators:

- **Filetype:** Directs Google to search only within the text of a particular type of file (for example, filetype:xls)
- **Inurl:** Directs Google to search only within the specified URL of a document (for example, inurl:search-text)
- **Link:** Directs Google to search within hyperlinks for a specific term (for example, link:www.domain.com)
- **Intitle:** Directs Google to search for a term within the title of a document (for example, intitle: “Index of /etc”)

By using these advanced operators in combination with key terms, both you and attackers can get Google to uncover many pieces of sensitive information that shouldn’t be revealed. These search strings are often called _Google dorks_.

To see how Google dorking works, enter the following phrase into Google:

**intext:JSESSIONID OR intext:PHPSESSID inurl:access.log ext:log**

This query searches in a URL for the session IDs that could be used to potentially impersonate users. It's not unusual for this search to find more than 100 sites that store sensitive session IDs in logs that were publicly accessible. If these IDs have not timed out, they could be used to gain access to restricted resources.

You can use advanced operators to search for many types of data. The following is another example of a Google search string (or Google dork) that can reveal passwords of web applications:

**"public $user =" | "public $password = " | "public $secret =" | "public $db =" ext:txt | ext:log -git**

Now that we have discussed some basic Google search techniques, let’s look at advanced Google hacking. We recommend that you visit the Google Hacking Database (GHDB) repositories at _[https://www.exploit-db.com/google-hacking-database/](https://www.exploit-db.com/google-hacking-database/)_. GHDB has the following search categories:

- Footholds
- Files containing usernames
- Sensitive directories
- Web server detection
- Vulnerable files
- Vulnerable servers
- Error messages
- Files containing juicy info
- Files containing passwords
- Sensitive online shopping info
- Network or vulnerability data
- Pages containing login portals
- Various online devices
- Advisories and vulnerabilities

![[Pasted image 20240717165037.png]]