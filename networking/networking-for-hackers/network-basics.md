# Network Basics

## Chapter 1: Network Basics

***

### IP Addresses

Internet Protocol addresses (IP addresses) make the world go 'round. Or, at least, enable us to email, Zoom, watch YouTube videos, Tweet, and navigate the web. It's almost as important as the world going around!

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Each digital device (computer, laptop, phone, tablet, etc.) is assigned an IP address, and this is what enables us to communicate and connect with it. Imagine an IP address as being similar to your house address. Without that address, no one could find you and send you snail mail.

The IP address system we are presently using is known as IP version 4, or IPv4. It is made up of 32 bits of four octets (8 characters) or four groups of 8 bits (on/off switches).

Take, for instance, 192.168.1.101. Each of the numbers between the dots (.) is the decimal equivalent of 8 bits. This means that we calculate the base 2 number (that computers use) represented by the 8 bits and convert them to decimal numbers that humans are more accustomed to working with (see the diagram below). Each one of the octets (8 bits) is capable of representing numbers within the range 0 through 255 (2 to the 8th power).

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

This is your private IP that is only usable on the local area network. To communicate over the internet, your IP address must be translated to a public IP by a NAT device (see NAT below).

### DHCP

Dynamic Host Configuration Protocol (DHCP) assigns IP addresses dynamically. This means that you do not have the same IP address all of the time. Most of the time, these IP address assignments are on a local area network. Remember, on LANs; we use private IP addresses.

When each device is connected to the LAN, it must request an IP address. That device sends the request to the DHCP server that assigns an IP address to that system for a fixed length of time, known as a "lease."

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Each time you connect to the LAN, you are likely to receive a different (dynamic) IP address, but usually in the same range. For instance, 192.168.0.0 - 192.168.255.255.

### NAT

Network Address Translation (NAT) is a protocol whereby internal private IP addresses are "translated" to an external public IP address that can be routed through the internet to its destination. Remember, private IP addresses of the systems inside the LAN cannot use their IP addresses on the internet because they are not unique (every LAN uses basically the same IP addresses inside their network).

The NAT device accepts requests to traverse the internet from an internal machine. It then records that machine's IP address in a table and converts the IP address to the external IP address of the router. When the packet returns from its destination, the NAT device looks into the saved table of the original request. It forwards the packet to the internal IP address of the system that made the original request within the LAN. When working properly, the individual systems and users don't realize this translation is taking place.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

For instance, the diagram above shows four computers with private IP addresses behind a device that is serving as both a NAT device and a router (not uncommon). The devices use their private IP addresses within the LAN, but when they want to communicate over the internet, the NAT device translates it to one of the public IP addresses that are unique on the internet. In this way, the routers along the way know exactly where to send the packets.

### Ports

Ports are a kind of sub-address. The IP address is the primary address, and the port is the sub-address. Using a well-worn but effective metaphor, think of the IP address as the street address of a building and then the port as the apartment number. I need the street address to get to the correct building, but I need the apartment address to find the individual person. This is similar to ports. The IP address gets us to the right host, but the port takes us to the proper service, say HTTP on port 80.

There are 65,536 (2 raised to the 16th power) ports. The first 1,024 are generally referred to as the "common ports." Obviously, people don't remember all 65,536 ports (unless they are savant) or even the 1,024 most common ports. As a hacker, security engineer, and/or network engineer, though, there are a few ports that you should know by heart.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

***

We can use a tool such as `Nmap` to see what ports are open on a system. In this way, the security engineer or hacker can see what ports are open and which services are running on the target system.

For instance, to see all the ports open on a Metasploitable-2 system (an intentionally vulnerable Linux system developed by the good people at Metasploit), we can run the following command:

```bash
kali > sudo nmap –sT <IP address of the target system>
```

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Arguably the two most important protocols for use over the internet are IP and TCP, so let's take a look at each of these.

***

### **IP (Internet Protocol)**

**IP**, or Internet Protocol, is the protocol that is used to define the source and destination IP address of a packet as it traverses the internet. It is often used in conjunction with other protocols such as TCP; hence, the often-used conjunction, TCP/IP.

Let's look at an IP packet header and see what information it contains that can be useful to the aspiring hacker and/or forensic investigator.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

* **Ring Topology:** In this topology, each node connects to exactly two other nodes, forming a single continuous pathway for signals through each node. The advantage is that it is relatively easy to install and reconfigure, but a break in any one of the connections can disrupt the entire network.

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

* **Star Topology:** This topology has each node connected to a central hub or switch, which acts as a repeater for data flow. It is the most common computer network topology today. Its main advantage is that it is easy to add or remove devices, and if one link fails, the others remain unaffected. However, the central hub represents a single point of failure.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

* **Mesh Topology:** This topology has each node connected to every other node, providing the most redundancy and reliability. The mesh network allows for continuous connections and reconfiguration around broken or blocked paths by “hopping” from node to node until the destination is reached. It is very robust and provides high redundancy but is the most costly and complex to install.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

* **Hybrid Topology:** This topology combines multiple topologies to leverage the strengths of each.

***

### **OSI Model**

The OSI and the TCP models are the most common models to understand the way that these various protocols work together. Many novices tend to minimize the importance of these models as they initially don’t seem to have any practical importance to networking systems. In reality, you should at least have a basic understanding of these models as you will hear references to them repeatedly in your career, such as, “this is a layer three switch.” This would be unintelligible without a rudimentary understanding of the OSI model.

Let’s begin with the OSI model. The diagram below displays the seven layers and the basic use of that layer in network communication.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

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

***

### **Why Sub-netting?**

Subnetting lets network administrators use the 32 bits in IPv4 IP address space more efficiently. They can create subnets within a Class A, B, or C network, enabling the administrator to create networks with more realistic host numbers.

Subnetting provides a flexible way to designate which portion of the IP address represents the host IP and which portion represents the network ID. Even if a single organization has thousands of devices, they don’t want them all running on the same network ID. The network would slow dramatically. By dividing up the network, you can have different physical networks and broadcast domains.

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

***

### **Subnets**

A subnet is a network within a network, namely a Class A, B, or C. Subnets are created by using one or more of the host bits to extend the network ID. As you know:

* **Class A networks** have an 8-bit network ID.
* **Class B networks** have a standard 16-bit network ID.
* **Class C networks** have a standard 24-bit network ID.

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Subnetting enables us to create network IDs of any size.

A network mask, or netmask, is a binary mask that is applied to an IP address to determine whether two IP addresses are in the same subnet. A network mask works by applying binary AND operations between the IP address and the mask.

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

***

#### **Subnet Masks**

Subnet masks use the 32-bit structure of the IP address. The subnet mask tells us which bits are for the Network ID and which bits are for the host ID. When the subnet mask bit is set to one, this means it is part of the network. A bit marked as zero is part of the host ID. The diagram below is meant to demonstrate this process of bit-wise AND operation between an IP address and its mask.

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

***

#### **CIDR Notation**

CIDR, or Classless Inter-Domain Routing notation, is a way of representing an IP address and the network mask associated with it. CIDR notation specifies an IP address, a slash (/), and a decimal number such as `192.168.1.0/24`, where the 24 represents the number of bits in the network mask. Of course, the number of bits can vary depending on the number of subnets.

***

#### **Our Scenario**

To demonstrate this principle, let's create a scenario. Assume we have a Class C network, say `192.168.1.0`. That means we have 254 host addresses available (1-254). What if we needed five different networks with no more than 30 hosts per network?

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

We can create smaller networks by borrowing bits from the host portion of the address.&#x20;

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

This provides us with a netmask like the one below.&#x20;

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

Those 3 bits would give us (2^3 = 8) (subtracting 2 for the reserved network and broadcast IP) subnets or 6. There would be 5 bits left in the network portion of the address or (2^5 = 32) (subtracting 2) or 30 hosts per subnet.

The calculation of the subnet mask after borrowing those 3 bits would be:

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

**2. `ping`**

The `ping` command checks the connectivity to a domain or IP address. It sends ICMP echo requests and receives echo replies.

```bash
kali > ping hackers-arise.com
```

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

* To ping by IP address:

```bash
kali > ping 185.230.63.107
```

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

**3. `netstat`**

`netstat` provides network statistics and information about network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.

* To show all connections:

```bash
kali > netstat -a
```

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

**4. `ss`**

`ss` is similar to `netstat` but provides more detailed information in a readable format.

```bash
kali > ss
```

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

* Simple Example :&#x20;

```
kali > ping 192.168.0.114
kali > tcpdump
```

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

As you can see, tcpdump displays the protocol (ICMP) and the type (echo request and echo reply). If we want to capture the output to a file where we can analyze it at a later time, we can use the –w option followed by the file name.

* To write capture to a file:

```bash
kali > tcpdump -w myoutput.cap
```

* To filter traffic by IP address:

```bash
kali > tcpdump host 192.168.0.114
```

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

* To filter traffic by port:

```bash
kali > tcpdump port 80
```

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

* To filter by TCP flags:

```bash
kali > tcpdump 'tcp[tcpflags] == tcp-syn'
```

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Note that we can see the three-way TCP handshake in the highlighted polygon. You can see first an “S” flag, then an “S.” flag (tcpdump represents the A or ACK flag with a “ .“), and then a “.” flag or written another way, S-SYN/ACK-ACK.

This filter displays traffic coming and going from our Windows 7 system. If we want to filter for just the traffic coming FROM our Windows 7 system, we can create a filter like;

```
kali > tcpdump src host 192.168.0.114
```

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

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

    <figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

* Filter by IP address:

```plaintext
ip.addr == 192.168.1.107
```

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

* Filter by port:

```plaintext
tcp.dstport == 80
```

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

* Filter for strings in payload:

```plaintext
tcp contains facebook
```

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

* Create filters using the Expression window:

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

* Follow a TCP stream by right-clicking a packet and selecting `Follow` > `TCP Stream`.

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

* This opens a pull-down window like that above. Click "Follow" and then "TCP Stream." :&#x20;

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

* Obtain statistics via `Statistics` > `IPv4 Statistics` > `All Addresses`.

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

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

**Exercises**

1. Create a firewall allowing access only to `hackers-arise.com` on ports `80` and `443`.
2. Add a rule to block port `445`.
3. Flush all rules to reset iptables configuration.

***

## Chapter 5: Wi-Fi Networks (802.11)
