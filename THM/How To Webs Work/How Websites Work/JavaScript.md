JS is one of the most popular coding languages in the world and allows pages to become interactive. HTML is used to create the website structure and content, while JavaScript is used to control the functionality of web pages - without JavaScript, a page would not have interactive elements and would always be static. JS can dynamically update the page in real-time, giving functionality to change the style of a button when a particular event on the page occurs (such as when a user clicks a button) or to display moving animations.

JavaScript is added within the page source code and can be either loaded within `<script>` tags or can be included remotely with the src attribute:

`<script src="/location/of/javascript_file.js"></script>`

[[HTML]] elements can also have events, such as "onclick" or "onhover" that execute JavaScript when the event occurs. The following code changes the text of the element with the demo ID to Button Clicked: 

`<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>` 
 Onclick events can also be defined inside the JavaScript script tags, and not on elements directly.