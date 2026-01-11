In many applications, the front-end server performs some rewriting of requests before they are forwarded to the back-end server, typically by adding some additional request headers. For example, the front-end server might:

- terminate the TLS connection and add some headers describing the protocol and ciphers that were used;
- add an `X-Forwarded-For` header containing the user's IP address;
- determine the user's ID based on their session token and add a header identifying the user; or
- add some sensitive information that is of interest for other attacks.

In some situations, if your smuggled requests are missing some headers that are normally added by the front-end server, then the back-end server might not process the requests in the normal way, resulting in smuggled requests failing to have the intended effects.

There is often a simple way to reveal exactly how the front-end server is rewriting requests. To do this, you need to perform the following steps:

- Find a POST request that reflects the value of a request parameter into the application's response.
- Shuffle the parameters so that the reflected parameter appears last in the message body.
- Smuggle this request to the back-end server, followed directly by a normal request whose rewritten form you want to reveal.

Suppose an application has a login function that reflects the value of the `email` parameter:

`POST /login HTTP/1.1 Host: vulnerable-website.com Content-Type: application/x-www-form-urlencoded Content-Length: 28 email=wiener@normal-user.net`

This results in a response containing the following:

`<input id="email" value="wiener@normal-user.net" type="text">`

Here you can use the following request smuggling attack to reveal the rewriting that is performed by the front-end server:

`POST / HTTP/1.1 Host: vulnerable-website.com Content-Length: 130 Transfer-Encoding: chunked 0 POST /login HTTP/1.1 Host: vulnerable-website.com Content-Type: application/x-www-form-urlencoded Content-Length: 100 email=POST /login HTTP/1.1 Host: vulnerable-website.com ...`

The requests will be rewritten by the front-end server to include the additional headers, and then the back-end server will process the smuggled request and treat the rewritten second request as being the value of the `email` parameter. It will then reflect this value back in the response to the second request:

`<input id="email" value="POST /login HTTP/1.1 Host: vulnerable-website.com X-Forwarded-For: 1.3.3.7 X-Forwarded-Proto: https X-TLS-Bits: 128 X-TLS-Cipher: ECDHE-RSA-AES128-GCM-SHA256 X-TLS-Version: TLSv1.2 x-nr-external-service: external ...`

#### Note

Since the final request is being rewritten, you don't know how long it will end up. The value in the `Content-Length` header in the smuggled request will determine how long the back-end server believes the request is. If you set this value too short, you will receive only part of the rewritten request; if you set it too long, the back-end server will time out waiting for the request to complete. Of course, the solution is to guess an initial value that is a bit bigger than the submitted request, and then gradually increase the value to retrieve more information, until you have everything of interest.

Example: 

CT-TE (Ensure to use auto update content length with this type of smuggling)
POST / HTTP/1.1
Host: 0ae7004c030e06e5812cbb3f00e60023.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 124
Transfer-Encoding: chunked

0

POST / HTTP/1.1
Content-Length: 200
Content-Type: application/x-www-form-urlencoded
Conntection: close

search=Test

and with this request we encounter the hidden header: X-UadyTt-Ip