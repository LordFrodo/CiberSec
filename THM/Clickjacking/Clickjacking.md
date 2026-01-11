Clickjacking is an interface-based attack in which a user is tricked into clicking on actionable content on a hidden website by clicking on some other content in a decoy website. Consider the following example:

A web user accesses a decoy website (perhaps this is a link provided by an email) and clicks on a button to win a prize. Unknowingly, they have been deceived by an attacker into pressing an alternative hidden button and this results in the payment of an account on another site. This is an example of a clickjacking attack. The technique depends upon the incorporation of an invisible, actionable web page (or multiple pages) containing a button or hidden link, say, within an iframe. The iframe is overlaid on top of the user's anticipated decoy web page content.

Example:
We use a iframe to have the same page with the actions that we want to execute and with CSS we transform it to look like a normal web page. In this case, we want to perform a delete account so, we will use a div tag with the text "Click me" to simulate a button, but the div tag will be in the same position as the original delete account button. Lets look at the html code:

<style> iframe { position:relative; width:$width_value; height: $height_value; opacity: $opacity; z-index: 2; } div { position:absolute; top:$top_value; left:$side_value; z-index: 1; } </style> <div>Test me</div> <iframe src="YOUR-LAB-ID.web-security-academy.net/my-account"></iframe>


If you have a input field like a username, email, password or something else, you can always try to poisoned in the url. Look at this example of poisoned a email in the url.

<iframe src="https://0a3100cd03b2bc7c80e9e45a00d50006.web-security-academy.net/my-account?email=test@a.comaa"></iframe>