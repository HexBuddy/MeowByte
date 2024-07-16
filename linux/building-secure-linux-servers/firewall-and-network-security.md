# Firewall and Network Security

#### Firewall and Network Security

**Table of Contents**

1. Cheat Sheet
2. Firewall Setup with UFW
3. Advanced Firewall Rules with iptables
4. Securing Network Services with TCP Wrappers
5. Securing IoT Devices on Linux Networks

***

## **Cheat Sheet**

| **Task**                     | **Command (Debian/Ubuntu)**                          | **Command (Arch Linux)**                             | **Command (CentOS/Red Hat)**                                       |
| ---------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------ |
| Install UFW                  | `sudo apt install ufw`                               | `sudo pacman -S ufw`                                 | `sudo yum install ufw` or `sudo dnf install ufw`                   |
| Enable UFW                   | `sudo ufw enable`                                    | `sudo ufw enable`                                    | `sudo ufw enable`                                                  |
| Allow a Port                 | `sudo ufw allow 22/tcp`                              | `sudo ufw allow 22/tcp`                              | `sudo ufw allow 22/tcp`                                            |
| Deny a Port                  | `sudo ufw deny 80/tcp`                               | `sudo ufw deny 80/tcp`                               | `sudo ufw deny 80/tcp`                                             |
| Check UFW Status             | `sudo ufw status`                                    | `sudo ufw status`                                    | `sudo ufw status`                                                  |
| Install iptables             | `sudo apt install iptables`                          | `sudo pacman -S iptables`                            | `sudo yum install iptables` or `sudo dnf install iptables`         |
| List iptables Rules          | `sudo iptables -L`                                   | `sudo iptables -L`                                   | `sudo iptables -L`                                                 |
| Add iptables Rule            | `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT` | `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT` | `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT`               |
| Save iptables Rules          | `sudo iptables-save > /etc/iptables/rules.v4`        | `sudo iptables-save > /etc/iptables/rules.v4`        | `sudo iptables-save > /etc/sysconfig/iptables`                     |
| Install TCP Wrappers         | `sudo apt install tcpd`                              | `sudo pacman -S tcp_wrappers`                        | `sudo yum install tcp_wrappers` or `sudo dnf install tcp_wrappers` |
| Configure `/etc/hosts.allow` | `ALL: LOCAL`                                         | `ALL: LOCAL`                                         | `ALL: LOCAL`                                                       |
| Configure `/etc/hosts.deny`  | `ALL: ALL`                                           | `ALL: ALL`                                           | `ALL: ALL`                                                         |
| Install VLAN utilities       | `sudo apt install vlan`                              | `sudo pacman -S vlan`                                | `sudo yum install vlan` or `sudo dnf install vlan`                 |
| Create a VLAN                | `sudo vconfig add eth0 10`                           | `sudo vconfig add eth0 10`                           | `sudo vconfig add eth0 10`                                         |

***

## Firewall Setup with UFW

Uncomplicated Firewall (UFW) is designed to simplify the process of configuring a firewall.

**Installing UFW**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install ufw
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S ufw
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install ufw
    ```

    or

    ```sh
    sudo dnf install ufw
    ```

**Basic UFW Commands**

UFW provides a straightforward way to manage firewall rules on Linux systems.

*   **Enable UFW**:

    ```sh
    sudo ufw enable
    ```
*   **Allow SSH Access**:

    ```sh
    sudo ufw allow ssh
    ```
*   **Allow HTTP and HTTPS**:

    ```sh
    sudo ufw allow http
    sudo ufw allow https
    ```
*   **Deny a Specific Port**:

    ```sh
    sudo ufw deny 80/tcp
    ```
*   **Check UFW Status**:

    ```sh
    sudo ufw status
    ```
*   **Disable UFW**:

    ```sh
    sudo ufw disable
    ```
*   **Reset UFW**:

    ```sh
    sudo ufw reset
    ```
*   **Enable Logging**:

    ```sh
    sudo ufw logging on
    ```
*   **Delete a Rule**:

    ```sh
    sudo ufw delete allow 22/tcp
    ```

**Configuring UFW**

UFW configuration files are typically located in `/etc/ufw`. Key files include `ufw.conf`, `before.rules`, `after.rules`, and `user.rules`.

*   **Example: Custom Rules**:

    ```sh
    sudo ufw allow from 192.168.1.0/24 to any port 3306
    ```
*   **Allow a Range of Ports**:

    ```sh
    sudo ufw allow 1000:2000/tcp
    ```
*   **Allow Specific IP Address**:

    ```sh
    sudo ufw allow from 192.168.1.100
    ```
*   **Deny Specific IP Address**:

    ```sh
    sudo ufw deny from 192.168.1.200
    ```

**Managing UFW Profiles**

UFW allows you to create profiles for different services, making it easier to manage firewall rules.

*   **Example: Create a Profile**:

    ```plaintext
    [MyApp]
    title=My Custom Application
    description=Allows traffic for MyApp
    ports=12345/tcp
    ```
*   **Enable the Profile**:

    ```sh
    sudo ufw allow MyApp
    ```
*   **Disable the Profile**:

    ```sh
    sudo ufw delete allow MyApp
    ```

***

## Advanced Firewall Rules with iptables

iptables provides granular control over network traffic by filtering and manipulating packets.

**Installing iptables**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install iptables
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S iptables
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install iptables
    ```

    or

    ```sh
    sudo dnf install iptables
    ```

**Basic iptables Commands**

iptables operates with tables (filter, nat, mangle) and chains (INPUT, OUTPUT, FORWARD).

*   **List Current Rules**:

    ```sh
    sudo iptables -L
    ```
*   **Add a Rule**:

    ```sh
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    ```
*   **Delete a Rule**:

    ```sh
    sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT
    ```
*   **Block Traffic from Specific IP**:

    ```sh
    sudo iptables -A INPUT -s 192.168.1.100 -j DROP
    ```
*   **Allow Established Connections**:

    ```sh
    sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    ```
*   **Log Dropped Packets**:

    ```sh
    sudo iptables -A INPUT -j LOG --log-prefix "Dropped: " --log-level 4
    ```
*   **Flush All Rules**:

    ```sh
    sudo iptables -F
    ```

**Creating Custom Rules**

Custom rules in iptables can specify source/destination addresses, ports, protocols, and actions.

*   **Example: Allow ICMP (Ping)**:

    ```sh
    sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
    ```
*   **Example: Rate Limiting**:

    ```sh
    sudo iptables -A INPUT -p tcp --dport 22 -m limit --limit 3/min --limit-burst 10 -j ACCEPT


    ```
*   **Example: Block Specific Subnet**:

    ```sh
    sudo iptables -A INPUT -s 192.168.1.0/24 -j DROP
    ```
*   **Example: Redirect HTTP to HTTPS**:

    ```sh
    sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 443
    ```

**Persisting iptables Rules**

iptables rules need to be saved to persist across reboots.

*   **Debian/Ubuntu**:

    ```sh
    sudo sh -c "iptables-save > /etc/iptables/rules.v4"
    sudo sh -c "ip6tables-save > /etc/iptables/rules.v6"
    ```
*   **Arch Linux**:

    ```sh
    sudo sh -c "iptables-save > /etc/iptables/iptables.rules"
    sudo sh -c "ip6tables-save > /etc/iptables/ip6tables.rules"
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo sh -c "iptables-save > /etc/sysconfig/iptables"
    sudo sh -c "ip6tables-save > /etc/sysconfig/ip6tables"
    ```

***

## Securing Network Services with TCP Wrappers

TCP Wrappers provide host-based access control for network services.

**Installing TCP Wrappers**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install tcpd
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S tcp_wrappers
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install tcp_wrappers
    ```

    or

    ```sh
    sudo dnf install tcp_wrappers
    ```

**Configuring TCP Wrappers**

Configuration files for TCP Wrappers are `/etc/hosts.allow` and `/etc/hosts.deny`.

*   **Allow Local Network**:

    ```plaintext
    ALL: LOCAL
    ```
*   **Block Specific IP**:

    ```plaintext
    ALL: 192.168.1.100
    ```
*   **Allow Specific Service**:

    ```plaintext
    sshd: 192.168.1.0/24
    ```
*   **Deny Specific Service**:

    ```plaintext
    telnetd: ALL
    ```
*   **Example `/etc/hosts.allow`**:

    ```plaintext
    ALL: 192.168.1.0/24
    ```
*   **Example `/etc/hosts.deny`**:

    ```plaintext
    ALL: ALL
    ```

**Examples of TCP Wrapper Rules**

*   **Allow Local Network**:

    ```plaintext
    ALL: LOCAL
    ```
*   **Block Specific IP**:

    ```plaintext
    ALL: 192.168.1.100
    ```
*   **Allow SSH for Specific Subnet**:

    ```plaintext
    sshd: 192.168.1.0/24
    ```
*   **Deny All Telnet Access**:

    ```plaintext
    telnetd: ALL
    ```
*   **Allow Specific Host**:

    ```plaintext
    ALL: 192.168.1.101
    ```

***

## Securing IoT Devices on Linux Networks

IoT devices require special considerations for network security due to their typically limited security features.

**Best Practices for IoT Security**

1. **Change Default Passwords**: Always change default login credentials.
2. **Firmware Updates**: Regularly update the firmware to patch vulnerabilities.
3. **Network Segmentation**: Use VLANs to isolate IoT devices from sensitive networks.
4. **Strong Encryption**: Enable strong encryption for communication (e.g., WPA3 for Wi-Fi).

**Setting Up VLANs for IoT Devices**

*   **Install VLAN Utilities**:

    ```sh
    sudo apt install vlan
    ```
*   **Create a VLAN**:

    ```sh
    sudo vconfig add eth0 10
    sudo ifconfig eth0.10 192.168.10.1/24 up
    ```
*   **Add VLAN Interface to `/etc/network/interfaces`**:

    ```plaintext
    auto eth0.10
    iface eth0.10 inet static
        address 192.168.10.1
        netmask 255.255.255.0
    ```
*   **Bring Up the VLAN Interface**:

    ```sh
    sudo ifup eth0.10
    ```

**Monitoring and Logging IoT Traffic**

Use tools like `tcpdump` and `Wireshark` to monitor and log network traffic.

*   **Example: Capture Traffic with tcpdump**:

    ```sh
    sudo tcpdump -i eth0 -w iot_traffic.pcap
    ```
*   **Example: Filter by IP Address**:

    ```sh
    sudo tcpdump -i eth0 host 192.168.1.50 -w iot_traffic_host50.pcap
    ```
*   **Example: Capture Specific Port**:

    ```sh
    sudo tcpdump -i eth0 port 80 -w iot_http_traffic.pcap
    ```
*   **Analyze with Wireshark**:

    ```sh
    wireshark iot_traffic.pcap
    ```
*   **Real-time Monitoring with tshark**:

    ```sh
    sudo tshark -i eth0
    ```

By implementing these firewall and network security measures, you can significantly enhance the security of your Linux systems and IoT devices. Each section provides detailed commands, configuration tips, and best practices to ensure robust protection and effective management of your network infrastructure.
