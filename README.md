# Netpractice

## Intoduction

This project is a general practical exercise to let you discover networking.
You will have to configure small-scale networks. To do so, it will be necessary to understand this concepts.

*  [Important concepts](#important-concepts)
    *    [TCP](#tcp)  
    *    [IP address](#ip-address)
    *    [Subnet mask](#subnet-mask)
    *    [Switch](#switch)
    *    [Router](#router)

You will have to complete 10 levels :   [Levels](#levels)

## Important Concepts

### TCP

TCP stands for Transmission Control Protocol a communications standard that enables application programs and computing devices to exchange messages over a network. It is designed to send packets across the internet and ensure the successful delivery of data and messages over networks.

TCP organizes data so that it can be transmitted between a server and a client. It guarantees the integrity of the data being communicated over a network. Before it transmits data, TCP establishes a connection between a source and its destination, which it ensures remains live until communication begins. It then breaks large amounts of data into smaller packets, while ensuring data integrity is in place throughout the process, toensures end-to-end data delivery without loss any of data.
As a result, high-level protocols that need to transmit data all use TCP Protocol.Examples include peer-to-peer sharing methods like File Transfer Protocol (FTP), Secure Shell (SSH)...

### IP Address

IP is part of an internet protocol suite, which also includes the transmission control protocol. Together, these two are known as [TCP/IP](#TCP/IP). The internet protocol suite governs rules for packetizing, addressing, transmitting, routing, and receiving data over networks.

IP addressing is a logical means of assigning addresses to devices on a network. Each device connected to the internet requires a unique IP address.

An IP address has two parts; one part identifies the host such as a computer or other device, and the other part identifies the network it belongs to. TCP/IP uses a [subnet mask](#subnet-mask) to separate them.


### IPv4 vs. IPv6

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

### Switch


///////

A switch connects multiple devices together in a single network. Unlike a router, the switch does not have any interfaces since it only distibutes packets to its local network, and cannot talk directly to a network outside of its own.

↥ back to top

### Router

///////


Just as the switch connects multiple devices on a single network, the router connects multiple networks together. The router has an interface for each network it connects to.

Since the router separates different networks, the range of possible IP addresses on one of its interface must not overlap with the range of its other interfaces. An overlap in the IP address range would imply that the interfaces are on the same network.


### Routing Table
//////


A routing table is a data table stored in a router or a network host that lists the routes to particular network destinations. In NetPractice, the routing table consists of 2 elements:

Destination: The destination specifies a network address on which a host is the end target of the packets. The route of default or 0.0.0.0/0, is the route that takes effect when no other route is available for an IP destination address. The default route will use the next-hop address to send the packets on their way without giving a specific destination. The default route will match any network.

Next hop: The next hop refers to the next closest router a packet can go through. It is the IP address of the next router on the packet's way. Every single router maintains its routing table with a next hop address.

## Levels

<details>
 <summary>Level 1</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level1/level1.png?raw=true" alt="level1">
   <br>
   <br>
   
   **1.** Since *Client A* and *Client B* are on the same network, their IP address must represent the same network in accordance to the subnet mask.
<br>
The subnet mask is *255.255.255.0*, which means that the first 3 bytes of the IP address represent the network, and the 4th byte represents the host. Since we are on the same network, only the host can change. 
<br>
The solution will be anything in the range of **104.96.23.0 - 104.96.23.255** excluding the following 3:
* **104.96.23.0:** The first number in the range of hosts (0 in this case) represents the network and cannot be used by a host.
* **104.96.23.255:** The last number in the range of hosts (255 in this case) represents the broadcast address.
* **104.96.23.12:** This address is already used by the host *Client B*.

**2.** Same reasoning as *1.*, however the subnet mask is *255.255.0.0* in this case. The first 2 bytes of the IP address will represent the network; and the last 2 bytes, the host address.
<br>
The solution will be anything in the range of **211.191.0.0 - 211.191.255.255**, excluding:
* **211.191.0.0:** Represents the network address.
* **211.191.255.255:** Represents the broadcast address.
* **211.191.89.75:** Already taken by host *Client C*.
   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 2</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level2/level2.png?raw=true" alt="level2">
   <br>
   <br>
   
   **1.** Since *Client B* is on the same private network as *Client A*, they should have the exact same subnet mask.
<br>
The solution can only be **255.255.255.224**.

**2.** To understand the subnet mask of *255.255.255.224*, let's look at it in binary form, along with the IP *192.168.20.222* of *Client B*:

<center>

```
MASK: 11111111.11111111.11111111.11100000
IP:   11000000.10101000.00010100.11011101
```
</center>
As we can see, the first 27 bits represent the IP address, while only the last 5 bits represent the host address.
<br>
All these 27 bits representing the network must stay the same in the IP addresses of hosts on the same network. To get the answer, we can only change the last 5 bits.
<br>
<br>
The answer is in the range of:

```
BIN:  11000000.10101000.00010100.11000000 - 11000000.10101000.00010100.11011111
or
DEC:  192.168.20.192 - 192.168.20.223
```
Excluding:
<br>
* **11000000.10101000.00010100.11000000:** Represents the network address (notice all 0 in the last 5 bits).
* **11000000.10101000.00010100.11011111:** Represents the broadcast address (notice all 1 in the last 5 bits).
* **11000000.10101000.00010100.11011110:** *Client B* already has that address.

**3.** Here we are introduced to the slash "/" notation for the subnet mask on *Interface D1*. A subnet mask of */30* means that the first 30 bits of the IP address represent the network address, and the remaining 2 bits represent the host address:
<center>

```
Mask /30: 11111111.11111111.11111111.11111100
```
</center>

We can see that this binary number corresponds to the decimal *255.255.255.252*, therefore it is identical to the mask found on *Interface C1*.
<br>
<br>
The answers can then be any addresses, as long as they meet the following conditions:
* The network address (first 30 bits) must be identical for *Client D* and *Client C*.
* The host bits (last 2 bits) cannot be all 1, nor all 0.
* *Client D* and *Client C* do not have identical IP addresses.
   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 3</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level3/level3.png?raw=true" alt="level3">
   <br>
   <br>
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 4</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level4/level4.png?raw=true" alt="level4">
   <br>
   <br>
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 5</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level5/level5.png?raw=true" alt="level5">
   <br>
   <br>
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 6</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level6/level6.png?raw=true" alt="level6">
   <br>
   <br>
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 7</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level7/level7.png?raw=true" alt="level7">
   <br>
   <br>
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 8</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level8/level8.png?raw=true" alt="level8">
   <br>
   <br>
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 9</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level9/level9.png?raw=true" alt="level9">
   <br>
   <br>
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 10</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level10/level10.png?raw=true" alt="level10">
   <br>
   <br>
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>
