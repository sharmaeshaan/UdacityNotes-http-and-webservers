# Course: HTTP and Web Servers

## Lesson: Requests and Responses
**Instructor: Karl Krueger**

### Module: Introduction

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

### Module: Your First Web Server

- A server is basically a program which waits for other programs to connect to it.
- Akin to a phone conversation, when a program gets connected to a server, a series of requests and responses beigns.
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


### Module: Parts of a URL




### Module: Hostnames and Ports




### Module: HTTP GET Requests




### Module: HTTP Responses

## Lesson:
**Instructor: **

### Module:



### Module:



### Module:



### Module:



### Module:



### Module:
