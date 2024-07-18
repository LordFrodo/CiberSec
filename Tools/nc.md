Netcat or simply `nc` has different applications that can be of great value to a pentester. Netcat supports both TCP and UDP protocols. It can function as a client that connects to a listening port; alternatively, it can act as a server that listens on a port of your choice. Hence, it is a convenient tool that you can use as a simple client or server over TCP or UDP.

First, you can connect to a server, as you did with Telnet, to collect its banner using `nc MACHINE_IP PORT`, which is quite similar to our previous `telnet MACHINE_IP PORT`. Note that you might need to press SHIFT+ENTER after the GET line.

Pentester Terminal

           `pentester@TryHackMe$ nc MACHINE_IP 80 GET / HTTP/1.1 host: netcat  HTTP/1.1 200 OK Server: nginx/1.6.2 Date: Tue, 17 Aug 2021 11:39:49 GMT Content-Type: text/html Content-Length: 867 Last-Modified: Tue, 17 Aug 2021 11:12:16 GMT Connection: keep-alive ETag: "611b9990-363" Accept-Ranges: bytes ...`
        

In the terminal shown above, we used netcat to connect to MACHINE_IP port 80 using `nc MACHINE_IP 80`. Next, we issued a get for the default page using `GET / HTTP/1.1`; we are specifying to the target server that our client supports HTTP version 1.1. Finally, we need to give a name to our host, so we added on a new line, `host: netcat`; you can name your host anything as this has no impact on this exercise.

Based on the output `Server: nginx/1.6.2` we received, we can tell that on port 80, we have Nginx version 1.6.2 listening for incoming connections.

You can use netcat to listen on a TCP port and connect to a listening port on another system.

On the _server_ system, where you want to open a port and listen on it, you can issue `nc -lp 1234` or better yet, `nc -vnlp 1234`, which is equivalent to `nc -v -l -n -p 1234`, as you would remember from the [Linux](https://tryhackme.com/module/linux-fundamentals) room. The exact order of the letters does not matter as long as the port number is preceded directly by `-p`.

|option|meaning|
|---|---|
|-l|Listen mode|
|-p|Specify the Port number|
|-n|Numeric only; no resolution of hostnames via DNS|
|-v|Verbose output (optional, yet useful to discover any bugs)|
|-vv|Very Verbose (optional)|
|-k|Keep listening after client disconnects|

Notes:

- the option `-p` should appear just before the port number you want to listen on.
- the option `-n` will avoid DNS lookups and warnings.
- port numbers less than 1024 require root privileges to listen on.

On the _client_-side, you would issue `nc MACHINE_IP PORT_NUMBER`. Here is an example of using `nc` to echo. After you successfully establish a connection to the server, whatever you type on the client-side will be echoed on the server-side and vice versa.

Consider the following example. On the server-side, we will listen on port 1234. We can achieve this with the command `nc -vnlp 1234` (same as `nc -lvnp 1234`). In our case, the listening server has the IP address `MACHINE_IP`, so we can connect to it from the client-side by executing `nc MACHINE_IP 1234`. This setup would echo whatever you type on one side to the other side of the TCP tunnel. You can find a recording of the process below. Note that the listening server is on the left side of the screen.