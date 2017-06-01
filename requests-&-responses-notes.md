# Course: HTTP and Web Servers

## Lesson: Requests and Responses
**Instructor: Karl Krueger**

### Module 1: Introduction

#### HTTP
- HTTP: Hyper Text Transfer/Transport Protocol
- A web browser and a web server communicate with each other by following a set of rules or a protocol, known as HTTP.

#### urllib
The `urllib` library in Python can parse components of a URL. For example:

```python
>>> from urllib.parse import urlparse
>>> var = urlparse('https://classroom.udacity.com/courses/ud303').path
>>> print(var)
courses/ud303
```

#### nmap
- `nmap` is a command line based application for network analysis and testing.
- Installation on Linux through `sudo apt install nmap`
- `ncat` is a part of the `nmap` toolkit which can be used to create simple servers and clients below the HTTP layer.
- The network layer below HTTP is called TCP - Transmission Control Protocol.
- We can use `ncat` to create a simple "send and receive" cycle between a basic server and a client. For example:

Open terminal and create a server at port 9999 and start listening for connections
```
ncat -l 9999
```
Open another terminal and create a local client and connect to the port of the server
```
ncat localhost 9999
```
Since a connection is established, typing anything in each terminal will lead to the text being sent back and forth between the "server" and the "client"

---
#### Helpful Links
- https://docs.python.org/3/library/urllib.html
- https://docs.python.org/3/library/urllib.parse.html#module-urllib.parse
- https://nmap.org/
- https://en.wikipedia.org/wiki/Transmission_Control_Protocol
---

### Module 2: Your First Web Server

- A server is basically a program which waits for other programs to connect to it.
- Akin to a phone conversation between two people, when a program connects to a server, a series of requests and responses beigns.
- The program connecting to a server and requesting it for data is called a "client".
- For every "request" that a client sends it, the server sends back a "response" containing the requested data.
- This "transaction" between the client and the server is called a "request-response cycle" and takes place within a set of rules, or a protocol, called HTTP.

- Web browsers like Firefox, Chrome, Internet Explorer, Safari, Opera are examples of HTTP clients.
- Web browsers are not the ONLY examples of HTTP clients, they're just the most common ones -- any program that interacts with another by sending requests is a client.

- While browsing a complex webpage with rich HTML, images, APIs and embedded elements, each HTTP transaction will consist of multipe requests and responses between the client and server.

- Any interaction with a webpage will involve HTTP. However, a low-level interaction like `ping` which does not involve interacting with webpages will not use HTTP.

#### Running Our Own Server
The `http` library of Python contains a module called `http.server` which can be used to quickly create and run simple web servers. For example:

Open terminal and start a server at port 8000
```python
python -m http.server 8000
```
*`python` initiates your default version of Python `-m` invokes the module `http.server` and `8000` is the port on which the server will run.*

Open a browser window and access the contents of this server
```
http://localhost:8000
```

The `localhost:8000` address shows the contents of whichever folder we initiate our server in. For example, if we open a terminal in the `Downloads` folder of our computer and initiate a server there, we will be able to see it's contents on `http://localhost:8000`

##### Error 404
If we attempt to open a file or folder which does not exist on our server, we will see an error message on our page, specifically `error code: 404`.

For example, if we initiate a server on port 8000 in your `Documents` folder which has the files `doc1.txt` and `doc2.txt`, the addresses `http://localhost:8000/doc1.txt` and `http://localhost:8000/doc2txt` will allow us to access those files. But if we type in the address `http://localhost:8000/doc3.txt` we will see an error page which tells us that no file was found at the provided address.

##### Port Numbers
We can set the server to whatever port number we want as long as the port number we choose is not in use by another app or service.

For example, instead of `8000` setting the port to `8464` with the statement `python -m http.server 8464` will also work just fine, which can then be accessed at `http://localhost:8464`

---
#### Helpful Links
- https://docs.python.org/3/library/http.html
- https://docs.python.org/3/library/http.server.html#module-http.server
- https://stackoverflow.com/questions/2200199/how-do-you-decide-what-port-to-use
---



### Module 3: Parts of a URL

- Web address is called a URI - Uniform Resource Identifier
- Every element which can be individually located on the web has a URI -- a unique string of text, numbers and special characters, which is called a URL -- Uniform Resource Locator.
- As the name says, it tells the browser exactly which resource to go to -- for example, a wikipedia page, a youtube video, a facebook profile etc.


- URL's are typically made up of several components
- Each component has it's own syntax
- Similar to "flags" in a Bash shell statement, many components of in a URL are optional, which is why URLs of different websites differ from each other.
- Typical URL example:
https://en.wikipedia.org/wiki/Prague
`https` is the scheme `en.wikipedia.org` is the hostname of the server and `wiki/Prague` is the directory path.

#### scheme
- A scheme is the is the protocol which tells the cilent i.e. the brower what protocol to follow when accessing the resource at the given url
- `https` and `http` are the most used schemes when accessing webpages... `file` is used when accessing resources on our own computer through the browser... `mailto` for links to email addresses... Google Chrome uses 'chrome' when accessing it's internal pages like settings and extensions... The scheme for bitcoin transactions is `bitcoin`...
- There are hundreds of URI schemes the list of which can be found at https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml

- *The primary difference between `http` and `https` is that of encryption. All requests and responses happening within a `https` protocol are encrypted while those within `http` are not*

#### hostname
- A hostname is a unique identifier for which tells the client which server to connect to. For example `localhost` or `www.wikipedia.com'
- A `:` always comes after the scheme
- A `//` always comes before a hostname and a single '/' immediately after it to indicate the beginning of a path
- If we don't enter a path after the hostname, the server will show us the `root` or the entry point of it's resources. On the web, this will typically be a website's homepage. On a local file system, this will be the main directory in which the server has been initiated.
- Since the `mailto` scheme only requires an email address and not a hostname, it can be written as `mailto:myname@mailservice.com`
- It is essential to mention schemes while typing URLs in HTML. For example, HTML will not identify `www.facebook.com` but `https://www.facebook.com` will give you a working link.

#### path
- The path is what identifies a specific resource on a server
- The syntax of the path varies depending on the host and the requested resource
- For example:
- the URL `https://upload.wikimedia.org/wikipedia/commons/d/d4/N.Tesla.JPG` with path `wikipedia/commons/d/d4/N.Tesla.JPG` takes us to an image file `N.Tesla.JPG`
which means that the server has a file with that name.
- but the URL `https://www.google.com/#q=cats` with the path `#q=cats` takes us to a webpage which shows us a list of Google search results -- which means there is no file named `#q=cats` on the server.
- So the path of a URL does not necessarily indicate the directory structure of a server or a the exact location of a praticular file -- it could also indicate a command/query which a program on the server can interpret in a particular way to show the user relevant results. In the case of a Google search, the server is most likely using the path `#q=cats` to query a database, extract links related to cats from it, insert them in a pretty webpage and send it back to the client.

##### URL reference

A URL reference is indicated by a `#` called a "fragment". URLs with fragments in them don't lead to a new resource on the server but rather a different element on the same webpage. For example, the URL `https://en.wikipedia.org/wiki/Prague#Geography` with the fragment `#Geography` will lead us to the section on the page with the HTML `<id = "Geography">`

---
#### Helpful Links
- https://en.wikipedia.org/wiki/Uniform_Resource_Identifier#Examples
- https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml
- https://support.google.com/webmasters/answer/70897?hl=en#3

---







### Module 4: Hostnames and Ports

- A "host" is a computer on the network which hosts a service that clients can connect to
- Every host has a unique hostname and every hostname has a unique IP address
- The hostname in a url tells the browser which server it should connect to
- Whenever we type an address into our browser, it translates the hostname to an IP address of the server and the port number on which the website or resource is located (somewhat similar to `localhost:8000`).
- A port number is essential to identify exactly which website you want to land up on since a single server could be serving up different services on different ports
- The mapping of hostnames with their IP addresses is maintained on DNS (Domain Name Service) servers by ISPs (Internet Service Providers)

#### `host` and `nslookup`

`host` and `nslookup` are programs which help us find out the network information related to a hostname. They can be especially helpful in finding out IP addresses. For example:

Open terminal and find out IP address of www.facebook.com with `host`

```
host www.google.com
```
```
www.facebook.com is an alias for star-mini.c10r.facebook.com.
star-mini.c10r.facebook.com has address 157.240.13.35
star-mini.c10r.facebook.com has IPv6 address 2a03:2880:f126:83:face:b00c:0:25de
```

Open terminal and find out IP address of www.facebook.com with `nslookup`

```
nslookup www.faceook.com
```
```
Non-authoritative answer:
www.facebook.com	canonical name = star-mini.c10r.facebook.com.
Name:	star-mini.c10r.facebook.com
Address: 157.240.13.35
```

#### IPv4 and IPv6
IPv4 is the older convention of IP addresses where a typical IP address is a 32-bit string and looks like `157.240.13.35`

IPv6 is the newer convention in which IP addresses are much longer 128-bit strings and typically look like `2404:6800:4009:806::200e`

The need for IPv6 arose when the internet started bursting at it's seams and started running out of unique number combinations for IP addresses. The longer, more complex IPv6 convention allows for a substantially larger pool of IP addresses, each with a unique number combination.

#### `localhost`

When we run a server on our computer it gets the hostname `localhost` with the IP address `127.0.0.1`, specifically, IPv4 address `127.0.0.1` and IPv6 address `::1`

#### Ports

- An IP address uniquely identifies a computer on a network. A **port** uniquely identifies a program on that computer.
- We don't need to mention the port number when visiting a website from our browser, because the browser can automatically interpret which port to send the request to based on the URL scheme.
    - `http` uses port number `80` and `https` uses port number `443` by default.
- When initiating a server locally, usually port number 8000 is used. `http://localhost:80` won't work since operating systems only allow the administrator / root account to use port numbers below `1024`.

---
#### Helpful Links
- https://www.quora.com/What-is-the-difference-between-host-and-server-in-terms-of-computer-networking
- http://mashable.com/2011/02/03/ipv4-ipv6-guide/#MDWZsJl18Oqw
- https://en.wikipedia.org/wiki/Port_(computer_networking)#Common_port_numbers
- https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers

---


### Module 5: HTTP GET Requests

There are different kinds of HTTP requests. Every request has a "method" or "verb" depending on what the client has requested from the server. The different types of HTTP methods are:
- `GET`
- `POST`
- `PUT`
- `PATCH`
- `DELETE`

#### `GET`

- The most commonly used HTTP method on the internet is `GET`.
- `GET` is used when a client requests a server to send over a copy of a resource, like a full webpage or image or video or results of a search query.

#### Typical `GET` Request

If we initialize a Python server in a local directory, go to it's IP address from the browser and click on any file or folder, we should see something like this in the open terminal window:

```
127.0.0.1 - - [01/Jun/2017 23:16:11] "GET /readme.md HTTP/1.1" 200 -
```
The above statement is a typical `GET` request made by a client. It's can be broken down into:
- `127.0.0.1`: The server IP address
- `[01/Jun/2017 23:16:11]`: Timestamp of the request
- `GET`: The HTTP request method
- `/readme.md`: Path of the requested resource, which in this case is a readme file
- `HTTP/1.1`: The protocol in use for the request and response. `1.1` is the version number of the protocol.

#### Manually Writing `GET` Request

The above example illustrated how a client automatically makes `GET` requests for us while we click and open resources. We can also write HTTP requests and get resources from a server manually using `ncat`, a tool in the `nmap` network analysis program.

Open terminal and start a server at port 8000
```
python -m http.server 8000
```
Open another terminal and start a connection to the server with `ncat`
```
ncat 127.0.0.1 8000
```
Once started, enter a `GET` request for any file or resource in the server directory and press `Enter` twice
```
GET /readme.txt HTTP/1.1
Host: localhost
```
We should get a response back from the server which looks like this:
```
HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.6.1
Date: Thu, 01 Jun 2017 18:11:53 GMT
Content-type: application/octet-stream
Content-Length: 1099
Last-Modified: Thu, 01 Jun 2017 10:02:22 GMT

Course notes jotted down while taking the ["HTTP & Web Servers"](https://www.udacity.com/course/http-web-servers--ud303) course on [Udacity](https://www.udacity.com/).
```

---
#### Helpful Links
- http://www8.org/w8-papers/5c-protocols/key/key.html
- https://en.wikipedia.org/wiki/HTTP/2
---






### Module 6: HTTP Responses


---
#### Helpful Links
---
