# Netpractice

## Table of Contents
*  [Important concepts](#important-concepts)
    *   [IP address](#ip-address)
    *    [Subnet mask](#subnet-mask)
    *    [Switch](#switch)
    *    [Router](#router)
*  [Levels](#levels)
```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
`red`## Important Concepts

- IP Address

////

IP is part of an internet protocol suite, which also includes the transmission control protocol. Together, these two are known as TCP/IP. The internet protocol suite governs rules for packetizing, addressing, transmitting, routing, and receiving data over networks.

IP addressing is a logical means of assigning addresses to devices on a network. Each device connected to the internet requires a unique IP address.

An IP address has two parts; one part identifies the host such as a computer or other device, and the other part identifies the network it belongs to. TCP/IP uses a subnet mask to separate them.


- IPv4 vs. IPv6

IP addresses come in 2 versions--IPv4 and IPv6:
/////


Internet Protocol version 4 (IPv4) defines an IP address as a 32-bit number. However, because of the growth of the Internet and the depletion of available IPv4 addresses, a new version of IP (IPv6), using 128 bits for the IP address, was standardized in 1998. However, only IPv4 addresses are used in NetPractice.


- Public Address vs. Private Address
A public IP address is an IP address that can be accessed directly over the internet and is assigned to your network router by your internet service provider (ISP). A public (or external) IP address helps you connect to the internet from inside your network, to outside your network.

A private IP address is the address your network router assigns to your device. Each device within the same network is assigned a unique private IP address (sometimes called a private network address) — this is how devices on the same internal network talk to each other.

When a network is connected to the internet, it cannot use an IP address from the reserved private IP addresses. The following ranges are reserved for private IP addresses:

```
192.168.0.0 – 192.168.255.255 (65,536 IP addresses)
172.16.0.0 – 172.31.255.255   (1,048,576 IP addresses)
10.0.0.0 – 10.255.255.255     (16,777,216 IP addresses)
↥ back to top
```
# Subnet Mask

///////


A subnet mask is a 32 bits (4 bytes) address used to distinguish between a network address and a host address in the IP address. It defines the range of IP addresses that can be used within a network or a subnet.


- Finding the network address
The Interface A1 above has the following properties:
```
IP address | 104.198.241.125
Mask       | 255.255.255.128  
```
To determine which portion of the IP address is the network address, we need to apply the mask to the IP address. Let's first convert the mask to its binary form:
```
Mask | 11111111.11111111.11111111.10000000
```
The bits of a mask that are 1 represent the network address, while the remaining bits of a mask that are 0 represent the host address. Let's now convert the IP address to its binary form:
```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```
We can now apply the mask to the IP address through a bitwise AND to find the network address of the IP:
```
Network address | 01101000.11000110.11110001.00000000
```
Which translates to a network address of `104.198.241.0`.


- Finding the range of host addresses
To determine what host addresses we can use on our network, we have to use the bits of our IP address dedicated to the host address. Let's use our previous IP address and mask:

```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```
The possible range of our host addresses are expressed through the last 7 bits of the mask which are all 0. Therefore, the range of host addresses is:
```
BINARY  | 0000000 - 1111111
DECIMAL | 0 - 127
```
To get the range of possible IP addresses for our network, we add the range of host address to the network address. Our range of possible IP addresses becomes `104.198.241.0 - 104.198.241.127`.

HOWEVER, the extremities of the range are reserved for specific uses and cannot be given to an interface:
```
104.198.241.0   | Reserved to represent the network address.
104.198.241.127 | Reserved as the broadcast address; used to send packets to all hosts of a network.
```
Therefore, our real IP range becomes `104.198.241.1 - 104.198.241.126`, which could have been found using an IP calculator.

* CIDR Notation (/24)
The mask can also be represented with the Classless Inter-Domain Routing (CIDR). This form represents the mask as a slash "/", followed by the number of bits that serve as the network address.

Therefore, the mask in the example above of `255.255.255.128`, is equivalent to a mask of /25 using the CIDR notation, since 25 bits out of 32 bits represent the network address.

↥ back to top

# Switch


///////

A switch connects multiple devices together in a single network. Unlike a router, the switch does not have any interfaces since it only distibutes packets to its local network, and cannot talk directly to a network outside of its own.

↥ back to top

# Router

///////


Just as the switch connects multiple devices on a single network, the router connects multiple networks together. The router has an interface for each network it connects to.

Since the router separates different networks, the range of possible IP addresses on one of its interface must not overlap with the range of its other interfaces. An overlap in the IP address range would imply that the interfaces are on the same network.


* Routing Table
//////


A routing table is a data table stored in a router or a network host that lists the routes to particular network destinations. In NetPractice, the routing table consists of 2 elements:

Destination: The destination specifies a network address on which a host is the end target of the packets. The route of default or 0.0.0.0/0, is the route that takes effect when no other route is available for an IP destination address. The default route will use the next-hop address to send the packets on their way without giving a specific destination. The default route will match any network.

Next hop: The next hop refers to the next closest router a packet can go through. It is the IP address of the next router on the packet's way. Every single router maintains its routing table with a next hop address.


