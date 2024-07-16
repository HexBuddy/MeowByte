# SSH and Remote Access Security

## **Table of Contents**

1. [Cheat Sheet](ssh-and-remote-access-security.md#cheat-sheet)
2. [Setting Up SSH for Secure Remote Access](ssh-and-remote-access-security.md#setting-up-ssh-for-secure-remote-access)
3. [Disabling Root Login over SSH for Security](ssh-and-remote-access-security.md#disabling-root-login-over-ssh-for-security)
4. [Secure Remote Access with OpenVPN](ssh-and-remote-access-security.md#secure-remote-access-with-openvpn)
5. [IPsec Configuration for Network Security](ssh-and-remote-access-security.md#ipsec-configuration-for-network-security)
6. [Setting Up a Tor Relay or Bridge](ssh-and-remote-access-security.md#setting-up-a-tor-relay-or-bridge)
7. [Using Tor for Anonymous Browsing](ssh-and-remote-access-security.md#using-tor-for-anonymous-browsing)

***

## **Cheat Sheet**

| **Task**                         | **Command (Debian/Ubuntu)**                             | **Command (Arch Linux)**                                  | **Command (CentOS/Red Hat)**                                           |
| -------------------------------- | ------------------------------------------------------- | --------------------------------------------------------- | ---------------------------------------------------------------------- |
| Install OpenSSH Server           | `sudo apt install openssh-server`                       | `sudo pacman -S openssh`                                  | `sudo yum install openssh-server` or `sudo dnf install openssh-server` |
| Start and Enable SSH Service     | `sudo systemctl start ssh && sudo systemctl enable ssh` | `sudo systemctl start sshd && sudo systemctl enable sshd` | `sudo systemctl start sshd && sudo systemctl enable sshd`              |
| Generate SSH Key Pair            | `ssh-keygen -t rsa -b 4096`                             | `ssh-keygen -t rsa -b 4096`                               | `ssh-keygen -t rsa -b 4096`                                            |
| Copy Public Key to Remote Server | `ssh-copy-id username@remote_host`                      | `ssh-copy-id username@remote_host`                        | `ssh-copy-id username@remote_host`                                     |
| Disable Root Login               | Edit `/etc/ssh/sshd_config`, set `PermitRootLogin no`   | Edit `/etc/ssh/sshd_config`, set `PermitRootLogin no`     | Edit `/etc/ssh/sshd_config`, set `PermitRootLogin no`                  |
| Install OpenVPN                  | `sudo apt install openvpn`                              | `sudo pacman -S openvpn`                                  | `sudo yum install openvpn` or `sudo dnf install openvpn`               |
| Install IPsec Tools              | `sudo apt install strongswan`                           | `sudo pacman -S strongswan`                               | `sudo yum install strongswan` or `sudo dnf install strongswan`         |
| Install Tor                      | `sudo apt install tor`                                  | `sudo pacman -S tor`                                      | `sudo yum install tor` or `sudo dnf install tor`                       |
| Start and Enable Tor Service     | `sudo systemctl start tor && sudo systemctl enable tor` | `sudo systemctl start tor && sudo systemctl enable tor`   | `sudo systemctl start tor && sudo systemctl enable tor`                |

***

## Setting Up SSH for Secure Remote Access

Secure Shell (SSH) provides a secure channel over an unsecured network. Here's how to set it up:

**Installing OpenSSH Server**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install openssh-server
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S openssh
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install openssh-server
    ```

    or

    ```sh
    sudo dnf install openssh-server
    ```

**Starting and Enabling SSH Service**

Ensure SSH starts on boot:

*   **All distributions**:

    ```sh
    sudo systemctl start sshd
    sudo systemctl enable sshd
    ```

**Basic Configuration**

Edit the SSH configuration file `/etc/ssh/sshd_config` for basic security settings.

*   **Example changes**:

    ```plaintext
    PermitRootLogin no
    PasswordAuthentication yes
    AllowUsers your_username
    ```
*   **Restart SSH service**:

    ```sh
    sudo systemctl restart sshd
    ```

**Generating SSH Key Pair**

SSH keys provide a secure method of logging into an SSH server without using a password.

*   **All distributions**:

    ```sh
    ssh-keygen -t rsa -b 4096
    ```
* Follow the prompts to set a file location and passphrase.

**Copying Public Key to Remote Server**

*   **All distributions**:

    ```sh
    ssh-copy-id username@remote_host
    ```
* Enter the remote user's password when prompted.

**Disabling Password Authentication**

After setting up key-based authentication, disable password authentication for added security.

1. Edit `/etc/ssh/sshd_config` and set `PasswordAuthentication no`.
   *   **Example**:

       ```plaintext
       PasswordAuthentication no
       ```
2.  Restart SSH service:

    ```sh
    sudo systemctl restart sshd
    ```

***

## Disabling Root Login over SSH for Security

Prevent root login over SSH to enhance security.

**Editing SSH Configuration**

1. Edit `/etc/ssh/sshd_config` and set `PermitRootLogin no`.
   *   **Example**:

       ```plaintext
       PermitRootLogin no
       ```
2.  Restart SSH service:

    ```sh
    sudo systemctl restart sshd
    ```

***

## Secure Remote Access with OpenVPN

OpenVPN provides a robust and secure way to create VPN tunnels.

**Installing OpenVPN**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install openvpn
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S openvpn
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install openvpn
    ```

    or

    ```sh
    sudo dnf install openvpn
    ```

**Configuring OpenVPN**

1. **Generate server and client certificates using Easy-RSA**:
   *   **Install Easy-RSA**:

       ```sh
       sudo apt install easy-rsa  # Debian/Ubuntu
       sudo pacman -S easy-rsa    # Arch Linux
       sudo yum install easy-rsa  # CentOS/Red Hat
       ```
   *   **Initialize Easy-RSA**:

       ```sh
       make-cadir ~/openvpn-ca
       cd ~/openvpn-ca
       source vars
       ./clean-all
       ./build-ca
       ./build-key-server server
       ./build-dh
       ./build-key client1
       ```
2. **Configure the server**:
   *   **Create a configuration file**:

       ```sh
       sudo cp /usr/share/doc/openvpn/examples/sample-config-files/server.conf /etc/openvpn/
       ```
   *   **Edit `/etc/openvpn/server.conf` to match your network settings**:

       ```plaintext
       port 1194
       proto udp
       dev tun
       ca ca.crt
       cert server.crt
       key server.key
       dh dh2048.pem
       ```
3. **Start and enable OpenVPN service**:
   *   **All distributions**:

       ```sh
       sudo systemctl start openvpn@server
       sudo systemctl enable openvpn@server
       ```

**Client Configuration**

1.  **Create a client configuration file**:

    ```plaintext
    client
    dev tun
    proto udp
    remote your_server_ip 1194
    resolv-retry infinite
    nobind
    user nobody
    group nogroup
    persist-key
    persist-tun
    ca ca.crt
    cert client1.crt
    key client1.key
    remote-cert-tls server
    cipher AES-256-CBC
    auth SHA256
    verb 3
    ```
2.  **Transfer the necessary files to the client**:

    ```sh
    scp /etc/openvpn/ca.crt /etc/openvpn/client1.crt /etc/openvpn/client1.key username@client_ip:/etc/openvpn/
    ```
3.  **Start the OpenVPN client**:

    ```sh
    sudo openvpn --config /etc/openvpn/client.conf
    ```

***

## IPsec Configuration for Network Security

IPsec provides secure IP communications by authenticating and encrypting each IP packet.

**Installing StrongSwan**

* \*\*Debian/Ubuntu

\*\*:

```sh
sudo apt install strongswan
```

*   **Arch Linux**:

    ```sh
    sudo pacman -S strongswan
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install strongswan
    ```

    or

    ```sh
    sudo dnf install strongswan
    ```

**Basic Configuration**

1.  **Edit the StrongSwan configuration file** `/etc/ipsec.conf`:

    ```plaintext
    config setup
      charondebug="ike 2, knl 2, cfg 2"

    conn %default
      keyexchange=ikev2
      authby=secret
      type=tunnel
      dpdaction=clear
      dpddelay=300s
      rekey=no

    conn myvpn
      left=%any
      leftid=@myvpnserver
      leftcert=serverCert.pem
      leftsendcert=always
      leftsubnet=0.0.0.0/0
      right=%any
      rightid=@myvpnclient
      rightauth=eap-mschapv2
      rightdns=8.8.8.8,8.8.4.4
      rightsourceip=10.0.0.0/24
      auto=add
    ```
2.  **Edit the authentication file** `/etc/ipsec.secrets`:

    ```plaintext
    : RSA serverKey.pem
    myvpnclient : EAP "clientpassword"
    ```
3.  **Start and enable StrongSwan service**:

    ```sh
    sudo systemctl start strongswan
    sudo systemctl enable strongswan
    ```

***

## Setting Up a Tor Relay or Bridge

Tor helps you maintain privacy and security on the internet.

**Installing Tor**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install tor
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S tor
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install tor
    ```

    or

    ```sh
    sudo dnf install tor
    ```

**Configuring Tor Relay**

1.  **Edit the Tor configuration file** `/etc/tor/torrc`:

    ```plaintext
    RunAsDaemon 1
    ORPort 9001
    DirPort 9030
    ExitPolicy reject *:*
    SocksPort 0
    Log notice file /var/log/tor/notices.log
    Nickname your_nickname
    ContactInfo your_email@example.com
    ```
2.  **Start and enable Tor service**:

    ```sh
    sudo systemctl start tor
    sudo systemctl enable tor
    ```

***

## Using Tor for Anonymous Browsing

Tor Browser allows you to browse the internet anonymously.

**Installing Tor Browser**

*   **Debian/Ubuntu**:

    ```sh
    sudo add-apt-repository ppa:micahflee/ppa
    sudo apt update
    sudo apt install torbrowser-launcher
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S torbrowser-launcher
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install torbrowser-launcher
    ```

    or

    ```sh
    sudo dnf install torbrowser-launcher
    ```

**Launching Tor Browser**

*   **All distributions**:

    ```sh
    torbrowser-launcher
    ```

***
