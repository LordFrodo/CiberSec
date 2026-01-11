**What is the DOM?**  

DOM stands for **D**ocument **O**bject **M**odel and is a programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style and content. A web page is a document, and this document can be either displayed in the browser window or as the HTML source. A diagram of the HTML DOM is displayed below:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/24a54ac532b5820bf0ffdddf00ab2247.png)  

If you want to learn more about the DOM and gain a deeper understanding [w3.org](https://www.w3.org/TR/REC-DOM-Level-1/introduction.html) have a great resource.

**Exploiting the DOM  
**

DOM Based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code. Execution occurs when the website JavaScript code acts on input or user interaction.  
  
  
**Example Scenario:**  
  
The website's JavaScript gets the contents from the `window.location.hash` parameter and then writes that onto the page in the currently being viewed section. The contents of the hash aren't checked for malicious code, allowing an attacker to inject JavaScript of their choosing onto the webpage.  
  
  
**Potential Impact:**  
  
Crafted links could be sent to potential victims, redirecting them to another website or steal content from the page or the user's session.

**How to test for Dom Based XSS:**

DOM Based XSS can be challenging to test for and requires a certain amount of knowledge of JavaScript to read the source code. You'd need to look for parts of the code that access certain variables that an attacker can have control over, such as "**window.location.x**" parameters.

  

When you've found those bits of code, you'd then need to see how they are handled and whether the values are ever written to the web page's DOM or passed to unsafe JavaScript methods such as **eval()**.


Examples:
1. If your payload is loaded on a image, you can use some of the image events to load your malicious payload. 
   `"><svg onload=alert(1)>`
    In this case, we are closing the path to load the image and added a svg onload event.
	 In the same case, we can use instead:
	 `" onload="alert(1)`
	 The " is used again to close the path of the image and we call the event onload but now of the img attribute.
	
2. On this case, we have a DOM XSS on a dropbox. Check the code 
	![[Pasted image 20250701103419.png]]
	In the Image, we notice that the document consults the select storeId, this item we can change it. If we add in the url the item storeId and assing any value, this value will be displayed as an option in the dropbox. 
	So, we can add a malicious payload in the value of the storeId. If we add this payload
	`test"></select><img%20src=""%20onerror=alert(1)>`
	With this payload, we close the select option from below and add and image that will run our code.
	Other way is use a svg item instead of a img, lets check the example
	`storeId=test"</select><svg%20onload=alert()>`



-----------------------------------------------
- jQuery DOM XSS

If a JavaScript library such as jQuery is being used, look out for sinks that can alter DOM elements on the page. For instance, jQuery's `attr()` function can change the attributes of DOM elements. If data is read from a user-controlled source like the URL, then passed to the `attr()` function, then it may be possible to manipulate the value sent to cause XSS. For example, here we have some JavaScript that changes an anchor element's `href` attribute using data from the URL:

`$(function() { $('#backLink').attr("href",(new URLSearchParams(window.location.search)).get('returnUrl')); });`

You can exploit this by modifying the URL so that the `location.search` source contains a malicious JavaScript URL. After the page's JavaScript applies this malicious URL to the back link's `href`, clicking on the back link will execute it:

`?returnUrl=javascript:alert(document.domain)`

Another potential sink to look out for is jQuery's `$()` selector function, which can be used to inject malicious objects into the DOM.

jQuery used to be extremely popular, and a classic DOM XSS vulnerability was caused by websites using this selector in conjunction with the `location.hash` source for animations or auto-scrolling to a particular element on the page. This behavior was often implemented using a vulnerable `hashchange` event handler, similar to the following:

`$(window).on('hashchange', function() { var element = $(location.hash); element[0].scrollIntoView(); });`

As the `hash` is user controllable, an attacker could use this to inject an XSS vector into the `$()` selector sink. More recent versions of jQuery have patched this particular vulnerability by preventing you from injecting HTML into a selector when the input begins with a hash character (`#`). However, you may still find vulnerable code in the wild.

To actually exploit this classic vulnerability, you'll need to find a way to trigger a `hashchange` event without user interaction. One of the simplest ways of doing this is to deliver your exploit via an `iframe`:

`<iframe src="https://vulnerable-website.com#" onload="this.src+='<img src=1 onerror=alert(1)>'">`

In this example, the `src` attribute points to the vulnerable page with an empty hash value. When the `iframe` is loaded, an XSS vector is appended to the hash, causing the `hashchange` event to fire.

If you find a JS thats use the replace funtion, check what items its going to change. In this example 
  function escapeHTML(html) {
        return html.replace('<', '&lt;').replace('>', '&gt;');
    }
This is a JavaScript `replace()` function to encode angle brackets. However, when the first argument is a string, the function only replaces the first occurrence. We exploit this vulnerability by simply including an extra set of angle brackets at the beginning of the comment. Something like this:
`<><img src=1 onerror=alert(1)>`

-----------------------------------------------
- AngularJS
If a framework like AngularJS is used, it may be possible to execute JavaScript without angle brackets or events. When a site uses the `ng-app` attribute on an HTML element, it will be processed by AngularJS. In this case, AngularJS will execute JavaScript inside double curly braces that can occur directly in HTML or inside attributes.
In your discovery time you find that your payloads are enclosed in an ng-app directive, you can try use this payload 
`{{$on.constructor('alert(1)')()}}`