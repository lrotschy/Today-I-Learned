1. **What is the internet?**
  The internet is a physical network of networks (including wires, routers, radio waves, etc.) that connects computers. It is also a design philosophy which is embodied in a set of protocols that determine how computers cooperate to use the physical network to send information. Protocols are rules of engagement that are agreed upon in advance and structure interaction. 
  The design of the internet allows it to be redundant, scalable, and decentralized, which makes it very reliable. Because it is decentralized, there is no one place where information is stored or actions are coordinated. It is redundant in that many machines and network connections can accomplish the same task. Decentralization and redundancy produce a system in which a breakdown in one are will not affect the whole--it is reliable. It also produces a system that is scalable. The network can expand without having to reconfigure the rest. In fact, the larger it gets, the more reliable and resilient it is.

3. **How does the internet work?**
A machine sends information in the form of bits through a physical medium to another machine. Bits are translated into radio, electric, or light waves, depending on the medium through which they are sent. 
4. **What is an IP address?**
And IP address is the location on the network where a computer is located. In the current system, and IP address is made up of 32 bits--4 numbers 0-255, separated by periods. The first is the country network, the second is the regional network, the third is the subnetwork, then the specific device. It can also include a port number--the specific endpoint on the machine.
05.155.36.124:80
IPV6 = 8 sets of hexadecimal characters, each containing 16 bits. First four are network, last four are interface
7. **What is a port number?**
A port number represents an endpoint on the machine. It identified a specific process/application that the message will be passed to. It is a 16 bit number. 80 is usually used for HTTP, 443 for HTTPS.
10. **What is DNS and how does it work?**
DNS stands for Domain Name System. URL's are human-friendly ways to identify the location of information on the internet; each URL has an associated IP address. DNS servers are connected in a distributed hierarchy divided into zones associated with .net, .edu, .com, etc. DNS servers store the IP addresses associated with URLs. When we enter a URL in a browser, we send a query to our local DNS server asking for the IP address of our URL. If it has it, it sends it back. Otherwise it sends the request to other servers in the DNS hierarchy until one has it and returns the information. Once our local computer has the IP address, then it can send a message to the appropriate location.
12. **Describe the client-server model of web interactions.**
The client-server model of web interactions is the idea of a client (e.g. browser or app) initiating a request-response cycle with a server. In the request, the client asks for the server to do something--often to share information in the form of a file--and the server responds--often by providing the resource requested. Each request/response cycle is independent. HTTP is the protocol used for the request and response communication.
14. **What is the role of HTTP protocol within the client-server model?**
HTTP is the protocol that structures interactions between clients and servers for the purpose of transmission of hypertext documents.
in web-based communication on the internet.
16. **Identify the components of a URL.**
http://www.example.com/home/:80?parameter=value&other_parameter=value 
`http` is the scheme, which identified the protocol 
`://` is syntax that divided the scheme from the rest
`www.example.com` is the host
`/home/` is the path
`:80` is the port This is optional
`?` is a reserved character that introduces a query string
`parameter=value `is a parameter name/value pair
`&` is a reserved character that introduces another search parameter/query string operator
17. **Construct a valid url. (use text and regex)**
```ruby
/\w+:\/\/(\w+.)+\.\w{3}(\/\w+)*(:\d{1,4})?(\?\w+=\w+\+?\w+(&\w+=\w+\+?\w+)?)?/
http://www.blah.com
https://poppy.blah.net/home/directory/elevators/hepc/
ftp://file.blah.edu:80
https://amazon.com?search=book+ruby&color=pink
http://amazon.com?search=book+ruby
```
19. **What is URL encoding and when might it be used?**
URLs only accept a proper subset of ASCII characters: 
unreserved = alphanumerics, -, ., _, ~
reserved/unsafe = :/?#[]@!$&'/*+,;=*$
All other characters must be encoded. Reserved or unsafe characters need not be encoded if being used for their special purpose.
To encode, replace character with % and the ASCII code. 
E.g. space = %20, # = %23, + = %23

20. **Explain HTTP requests and responses. Identify the components of each.**
Requests are set from the client to the server. Requests must include the HTTP method (a value that identified the type of request, e.g. GET, POST), host, and path. Optional parts of the request are the parameters, headers, and body.

Responses are sent from the server to the client. Responses must include a status code. Optional parts of a response are headers and body.

Headers are a string of comma-separated name/value pairs sent with a request or response that pass additional information. The body of the response is where the contents of a request or response are found, e.g. an HTML file, a value for a parameter.

When you click on a link or type a url into your browser you are sending a GET request to the server where the files for that website are stored. Your browser issues a GET request with the host and path of the file. Other information may be included as well in the headers. 

The server responds by sending back a response. The body of the response include the HTML file that your browser reads. The browser looks for any embedded files and issues GET requests for those as well behind the scenes. When they are received, they are rendered on your screen. If you need to enter information on a webpage, for example to sign in, your browser sends a POST request. The data you entered is included in the body of the request. The server may include a `Location` header in its response. This tells the browser to issue a GET request for that location. The effect is that after you successfully sign in, your browser loads the `location` page automatically.

22. **Describe the HTTP request/response cycle.**
The client sends a request.
The server responds to the request.
Uh... see codeacademy articles
23. **Explain what status codes are and provide examples.**
Status codes are required in a server's response to an HTTP request. They indicate the status of the request using a 3 digit code and a brief explanation of what the code means. 200 OK means that the request was fulfilled successfully. 404 Not found means that the file was not found on the server at the location specified in the path. 500 Server error means that there is a server side error and the request cannot be fulfilled until action is taken on the server side to correct the problem. 302 Found means that a file was not in the location indicated in the path but there was a successful redirect to its new location.
25. **Explain what 'state' means in context of the web.**
In this context 'state' means the condition of a program with respect to stored inputs. A program is stateful if it tracks and remembers inputs. A program is not stateful if it does not track and remember stored inputs. HTTP is stateless, but TCP is stateful. HTTP uses cookies and sessions to simulate statefulness, but each HTTP interaction is independent of the rest; each request must contain all the information it requires to be executed.

26. **What are some techniques used to simulate statefulness?**
Parameters, cookies, Ajax, session id and information.

Parameters are passed in the body of an HTTP request and used to execute the program from the server. 

Cookies are small pieces of data that are sent by the server and stored on the browser. They can be passed back and forth during request/response cycles. They are usually used for session management, personalization, and tracking user behavior.

Servers can also track session information. Cookies containing the session id are saved on the client side.Session information is saved on the server side and accessed using the session id. The server checks the session id and info on every request and recreates the application state every time, giving the appearance of statefulness. However, each request/response is independent.

Ajax stands for Asynchonous JavaScript and XML. It is a program that allows for asynchronous requests--the full web page is not regenerated with each request. This is accomplished with callbacks--a piece of logic that is designed to be exectued after another event. This makes each request/response cycle much less expensive.
- Parameters pass information to the server that can be used to change or set values. 
- Cookies are small pieces of data that are saved on the browser and used to save information. They are often used for session management, user behavior tracking, and personalization. 
- Sessions are records of interaction. A session id is saved in a cookie on the browser, and session information is stored on the server. In this way, the faux "state" can be recreated using the stored information every time the resource is requested.
- Ajax is used to cut down on the expense of recreating the resource with every request. It used callbacks to permit loading only a small part of a web page rather than the entire thing. 
28. **Explain the difference between GET and POST and when to use each.**
GET and POST are kinds of HTTP requests.
A GET request accesses resources stored on the server. We issue a GET request when we enter a url or click a link. More GET requests are issued by the browser for other resources such as images. Searches are also GET requests, despite the appearance of posting search terms.

A POST request submits input that changes values stored on the server. We use POST requests when we fill out a form. 
In a GET request, parameters are passed as part of an optional query string in the URL. In a POST request, they are included in the body.

30. **List security risks and countermeasures for each.**
There are many types of security risks. Some common ones are session hijacking and XSS--Cross-Site Scripting.

Session hijacking is when a hacker gets access to the session id. They can then issue their own request to the site using the session id. This allows them to access your personal information without knowing your password or username. Some countermeasures for session hijacking are to limit the length of sessions so that a hacker will only have access fora  limited amount of time; using HTTPS across a site so that every interaction is encrypted; resetting sessions--requiring a new session and reauthentication every time a client enters sensitive information.

XSS is a hacker technique that involves entering html or JavaScript code into comments or forms.The input becomes part of the page's contents. When another client requests the page, their browser executes the injected code, allowing the hacker to circumvent the same-origin policy. The malicious code can be destructive to the server or to other clients. Countermeasures include sanitizing input, for instance by eliminating all html tags, disallowing html and javscript in favor of markdown or other text, and by escaping all problematic characters so that they are interpreted as text rather than code.

30. **What is the Same Origin Policy?**

The same origin policy is a general security protocol that disallows access from one server and host to another. Applications must have the same protocol, hostname, and port number in order to have free access to one another.

CORS--Cross Origin Resource Sharing--is a mechanism that allows access to other resources not of the same origin by use of special headers.

[TCP/IP vs. OSI: What’s the Difference Between them?](https://community.fs.com/blog/tcpip-vs-osi-whats-the-difference-between-the-two-models.html)
"Considering the meanings of the two reference models, the OSI model is just a conceptual model. It is mainly used for describing, discussing, and understanding individual network functions. However, TCP/IP is firstly designed to solve a specific set of problems, not to function as a generation description for all network communications as OSI model. OSI model is generic, protocol independent, yet most protocols and systems adhere to it, while TCP/IP model is based on standard protocols which the Internet has developed. Another thing should be noted in OSI model is that not all layers are used in simpler applications. While the layers 1, 2, 3 are mandatory for any data communication, the application may use some unique interface layer to the application instead of the usual upper layers in the model."


Wikipedia
Same-origin policy
In computing, the same-origin policy is an important concept in the web application security model. Under the policy, a web browser permits scripts contained in a first web page to access data in a second web page, but only if both web pages have the same origin. An origin is defined as a combination of URI scheme, host name, and port number. This policy prevents a malicious script on one page from obtaining access to sensitive data on another web page through that page's Document Object Model.
This mechanism bears a particular significance for modern web applications that extensively depend on HTTP cookies to maintain authenticated user sessions, as servers act based on the HTTP cookie information to reveal sensitive information or take state-changing actions. A strict separation between content provided by unrelated sites must be maintained on the client-side to prevent the loss of data confidentiality or integrity.
The same-origin policy mainly applies to data access from scripts; embedding resources across origins, such as images, CSS and scripts via the corresponding HTML tags is not restricted (with fonts being a notable exception).
