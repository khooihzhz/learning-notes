# Socket Programming

``` python
import socket

s =  socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# bind addr, port
s.bind(('localhost', 1060))

```
### arguments
1. AF_INET = IPv4 / AF_INET6 = IPv6
2. SOCK_TYPE
	a. SOCK_STREAM = TCP
	b. SOCK_DGRAM = UDP
	c. SOCK_RAW = low level, bypass transport layer
3. PROTOCOL
	a. DEFAULT BASED on "SOCK_TYPE"


## get info from host 

``` python
# arguments 
socket.getaddrinfo(host, port, family=0, type=0, proto=0, flags=0)

info = socket.getaddrinfo('www.google.com', 'www')

```

returns 
![[Pasted image 20211122102109.png]]

can be accessed with TCP / UDP connection

