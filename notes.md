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
>>> from urllib.parse imort urlparse
>>> var = urlparse('https://classroom.udacity.com/courses/ud303').path
>>> print(var)
courses/ud303
```

#### nmap
- `nmap` is a command line based application for network analysis and testing. https://nmap.org/
- Installation on Linux through `sudo apt install nmap`
- `ncat` is a part of the `nmap` toolkit which can be used to create simple servers and clients below the HTTP layer.
- The network layer below HTTP is called TCP - Transmission Control Protocol. https://en.wikipedia.org/wiki/Transmission_Control_Protocol
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


### Module: Your First Web Server




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
