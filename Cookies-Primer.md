# Cookies

## What are cookies?
They are pieces of information that your browser stores. The information is set by the sites you visit. They contain all kinds of information: sessionId, ad tracking information, browsing preferences, shopping cart informations etc.
Because HTTP is a stateless protocol, information is stored client-side and used to create the appearance of statefulness.
How are they set, sent, stored?
Cookies are tiny text files that consist of key-value pairs and attributes.

They are set by a website. When a user makes a request to the website, a Set-Cookie response header can be sent back with the value for the cookie in a ‘Cookie’ header. The user’s browser stores the cookie and attached it as a header with every subsequent request.
Browsers set limits on the number of cookies a website can store on a user’s browser, usually 50. 

You can see the cookies that Chrome has set by clicking on the yellow arrow (used to be three dots) up on the URL bar next to your photo/initial. From there go to Privacy and Security > Site Settings > Cookies and site data > See all Cookies. You can look at individual cookies and see their attributes and other information, as well as manage them.

## What is their relationship with sessions?
A session is what it sounds like—it is a user’s interaction event or a series of connected interaction events—“a pool of data associated related to an active connection”. Session information is stored server-side. After a user is authenticated, a session is begun. The sessionId is saved server-side, often in a key-value store like Redis. A cookie is set with the sessionId. The sessionId is long, and pretty much impossible to guess. With each subsequent request to the website, the user’s browser sends back the sessionId. The server checks for the sessionId against stored values and then accesses the user’s stored information to provide the response. If the sessionId doesn’t exist, the user has to login and a new sessionId will be set. 
What attributes can you set on them?

Path: cookie will be sent only on requests that include the path value, so usually you want to set it to root. The default is whatever the path is when the cookie is set.
- path=/  

SameSite: prevents cookies from being sent with requests that are initiated by other sites. 
- SameSite=None — default, cookie is always sent, no restrictions
- SameSite=Lax — sends cookie on top-level requests that originate from another website, but not from subresource requests. This prevents Cross-Site Request Forgery, and should be the default.
- SameSite=Strict — Cookie is never sent with requests that originate from a different website

HttpOnly: Boolean value. If true, cookie will be sent with HTTP requests, but it will not be available from JavaScript inside a web page. Prevents Cross-Site Scripting attacks.

Secure: Cookie will only be sent over a secure connection. Should be set to true or it can be used to hijack a user’s session. Even better, use HTTPS for the entire site.

Expires: Sets expiration date. 30 days is common. To invalidate a cookie, set to a past date.


## A formula for a safe cookie:  
Set-Cookie: key=value; Secure; HttpOnly; Path=/; SameSite=Lax; Expires=Fri, 1 Nov 2019 00:00:00 GMT

In Express, API for working with cookies:

```
res.cookies(‘sessionId’, sessionId, {
Secure: true,
httpOnly: true,
sameSite: ‘lax’,
maxAge: 30 * 24 * 60 * 60 * 1000 // 30 days
})

res.clearCookie(‘sesssionId’, {
Secure: true,
httpOnly: true,
sameSite: ‘lax’
})
```

## JavaScript API for working with cookies

JavaScript API for interacting with cookies is stupid but there are libraries.

`document.cookie` returns all the cookies for the site—used in Cross-Site Scripting attacks for injecting JS code that sends cookie information to hackers, which is why your cookies should be HttpOnly.

To set: 
`document.cookie = ‘name=Feross’`
`document.cookie = ‘favoriteFood=Cookies; Path=/’`

To get--returns a semi-colon delimited string:

`document.cookie` 
// name=Feross; favoriteFood=Cookies;

To delete: 

`document.cookie = ‘name=; Expires=Thu, 01 Jan 1970 00:00:00 GMT’`

`document.cookie` 
`// favoriteFood=Cookies;`

## Further Reading
### From the Stanford MOOC on security:
https://www.youtube.com/watch?v=QuhgjXKzfI8
https://www.youtube.com/watch?v=0-q69vAYSwo&t=264s

https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview
https://web.dev/samesite-cookies-explained/
https://tools.ietf.org/html/draft-west-cookie-incrementalism-00#section-4.1
https://scotthelme.co.uk/csrf-is-dead/
https://tools.ietf.org/html/draft-west-cookie-incrementalism-00#section-4.1
https://web.dev/samesite-cookies-explained/

### Other Reading:
https://humanwhocodes.com/blog/2009/05/05/http-cookies-explained/
https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/cookies/Cookie
https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
https://developer.mozilla.org/en-US/docs/Web/HTTP

### Cookies vs. Sessions:
https://web.stanford.edu/~ouster/cgi-bin/cs142-fall10/lecture.php?topic=cookie
https://www.tutorialspoint.com/What-is-the-difference-between-session-and-cookies
