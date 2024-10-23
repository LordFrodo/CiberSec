frida -f owasp.sat.agoat -l root_bypass.js -U
-l is the script that i want to run
-U is to run on the USB or virtual device
-f to specify the application binary, 

Use Frida codeshare to find some usefull scripts

And example to run it is this one:

$ frida --codeshare dzonerzy/fridantiroot -f YOUR_BINARY

objection -g owasp.sat.agoat explore
-g to specify the application binary
Run help android to saw all the available commands to run