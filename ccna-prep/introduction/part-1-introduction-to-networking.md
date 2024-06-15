# Part 1 – Introduction to Networking

## Chapter 1 – Introduction to TCP/IP Networking

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

The five layer TCP/IP model splits the four layer model’s Network Access layer into separate Physical and Data-Link layers.

The CCNA 200-301 exam uses the RFC 1122 four layer TCP/IP model.

## Chapter 2 – Fundamentals of Ethernet LANs

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

MAC address: `OU:IO:UI:VE:ND:OR`

OUI – Organisationally Unique Identifier – ID assigned to a particular manufacturer VENDOR – managed and assigned by the manufacturer

CSMA/CD (Carrier sense multiple access with collision detection) – if the sender detects a collision, it sends a jamming signal. All nodes cease transmitting and resume it after a random time.

Wires used in 10BASE-T and 100BASE-T: 1,2,3,6.

Crossover cable: `1→3, 2→6, 3→1, 6→2`

Wires used in 1000BASE-T: `1-8.`

#### Ethernet II frame:

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

Multicast MAC addresses: `01:00:5E:00:00:00-01:00:5E:7F:FF:FF`

The last 23 bits of a multicast MAC address are used to map the relevant multicast IP address. Since multicast addresses have 28 variable bits, this is a one-to-many mapping, i.e. one MAC address is used for several (32 to be precise) IP addresses.

## Chapter 3 – Fundamentals of WANs and IP Routing

High-Level Data Link Control (HDLC) – Point-to-point layer 2 protocol

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>
