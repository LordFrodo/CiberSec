As same as DIRB, Gobuster is a tool to get any subdomain that the web application has. In this tool you can pass any list that u had downloaded, so in some cases those lists doesnt have any word that match with a subdomain, so is recommendable to use another list or tool to be more accurate.

Code Example: gobuster dir -u http://10.10.82.0.22/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt   

you can use "-x" to filter the output to only file with the extension that you wrote. Example: gobuster dir -u http://10.10.82.0/ -w UploadVulnsWordlist_1593564107766.txt -x jpg

Now let's run Gobuster with a wordlist using `gobuster dir -u http://10.10.15.29:3333 -w` .

|                   |                                           |
| ----------------- | ----------------------------------------- |
| **Gobuster flag** | **Description**                           |
| -e                | Print the full URLs in your console       |
| -u                | The target URL                            |
| -w                | Path to your wordlist                     |
| -U and -P         | Username and Password for Basic Auth      |
| -p **<x>**        | Proxy to use for requests                 |
| -c <http cookies> | Specify a cookie for simulating your auth |