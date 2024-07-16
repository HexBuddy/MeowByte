# SSH and Remote Access Security

## SSH and Remote Access Security

### Table of Contents

1. [Cheat Sheet](ssh-and-remote-access-security.md#cheat-sheet)
2. [Setting Up SSH for Secure Remote Access](ssh-and-remote-access-security.md#setting-up-ssh-for-secure-remote-access)
3. [Disabling Root Login over SSH for Security](ssh-and-remote-access-security.md#disabling-root-login-over-ssh-for-security)
4. [Secure Remote Access with OpenVPN](ssh-and-remote-access-security.md#secure-remote-access-with-openvpn)
5. [IPsec Configuration for Network Security](ssh-and-remote-access-security.md#ipsec-configuration-for-network-security)
6. [Setting Up a Tor Relay or Bridge](ssh-and-remote-access-security.md#setting-up-a-tor-relay-or-bridge)
7. [Using Tor for Anonymous Browsing](ssh-and-remote-access-security.md#using-tor-for-anonymous-browsing)

***

### Cheat Sheet

| Task                                 | Command (Debian/Ubuntu)                                 | Command (Arch Linux)                                      | Command (CentOS/Red Hat)                                                                                  |
| ------------------------------------ | ------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Install OpenSSH Server**           | `sudo apt install openssh-server`                       | `sudo pacman -S openssh`                                  | <p><code>sudo yum install openssh-server</code><br>or<br><code>sudo dnf install openssh-server</code></p> |
| **Start and Enable SSH Service**     | `sudo systemctl start ssh && sudo systemctl enable ssh` | `sudo systemctl start sshd && sudo systemctl enable sshd` | `sudo systemctl start sshd && sudo systemctl enable sshd`                                                 |
| **Generate SSH Key Pair**            | `ssh-keygen -t rsa -b 4096`                             | `ssh-keygen -t rsa -b 4096`                               | `ssh-keygen -t rsa -b 4096`                                                                               |
| **Copy Public Key to Remote Server** | `ssh-copy-id username@remote_host`                      | `ssh-copy-id username@remote_host`                        | `ssh-copy-id username@remote_host`                                                                        |
| **Disable Root Login**               | Edit `/etc/ssh/sshd_config`, set `PermitRootLogin no`   | Edit `/etc/ssh/sshd_config`, set `PermitRootLogin no`     | Edit `/etc/ssh/sshd_config`, set `PermitRootLogin no`                                                     |
| **Install OpenVPN**                  | `sudo apt install openvpn`                              | `sudo pacman -S openvpn`                                  | <p><code>sudo yum install openvpn</code><br>or<br><code>sudo dnf install openvpn</code></p>               |
| **Install IPsec Tools**              | `sudo apt install strongswan`                           | `sudo pacman -S strongswan`                               | <p><code>sudo yum install strongswan</code><br>or<br><code>sudo dnf install strongswan</code></p>         |
| **Install Tor**                      | `sudo apt install tor`                                  | `sudo pacman -S tor`                                      | <p><code>sudo yum install tor</code><br>or<br><code>sudo dnf install tor</code></p>                       |
| **Start and Enable Tor Service**     | `sudo systemctl start tor && sudo systemctl enable tor` | `sudo systemctl start tor && sudo systemctl enable tor`   | `sudo systemctl start tor && sudo systemctl enable tor`                                                   |

***

## Setting Up SSH for Secure Remote Access

**SSH (Secure Shell)** is a protocol that provides a secure way to access a remote computer over an unsecured network. It uses encryption to protect data transmitted over the network, ensuring confidentiality and integrity.

#### Installing OpenSSH Server

**OpenSSH** is a suite of secure networking utilities based on the Secure Shell protocol, which provides encrypted communication sessions over a computer network.

**Debian/Ubuntu:**

```bash
sudo apt install openssh-server
```

**Arch Linux:**

```bash
sudo pacman -S openssh
```

**CentOS/Red Hat:**

```bash
sudo yum install openssh-server
# or
sudo dnf install openssh-server
```

#### Starting and Enabling SSH Service

Ensure SSH starts on boot so you can access your server remotely anytime it is powered on.

**All distributions:**

```bash
sudo systemctl start sshd
sudo systemctl enable sshd
```

* `systemctl start sshd`: Starts the SSH service.
* `systemctl enable sshd`: Ensures the SSH service starts automatically at boot.

#### Basic Configuration

Editing the SSH configuration file `/etc/ssh/sshd_config` enhances the security of the SSH service.

**Example changes:**

```bash
PermitRootLogin no
PasswordAuthentication yes
AllowUsers your_username
```

* `PermitRootLogin no`: Disables root login over SSH, reducing the risk of brute-force attacks on the root account.
* `PasswordAuthentication yes`: Allows password-based authentication.
* `AllowUsers your_username`: Restricts SSH access to specific users.

Restart SSH service to apply changes:

```bash
sudo systemctl restart sshd
```

#### Generating SSH Key Pair

SSH keys provide a secure method of logging into an SSH server without using a password, which is more secure than password-based authentication.

**All distributions:**

```bash
ssh-keygen -t rsa -b 4096
```

* `-t rsa`: Specifies the type of key to create, in this case, RSA.
* `-b 4096`: Specifies the number of bits in the key, in this case, 4096 bits.

Follow the prompts to set a file location and passphrase.

#### Copying Public Key to Remote Server

This command copies your public key to the remote server, allowing you to log in without a password.

**All distributions:**

```bash
ssh-copy-id username@remote_host
```

Enter the remote user’s password when prompted.

#### Disabling Password Authentication

After setting up key-based authentication, disable password authentication for added security.

Edit `/etc/ssh/sshd_config` and set `PasswordAuthentication no`.

**Example:**

```bash
PasswordAuthentication no
```

Restart SSH service to apply changes:

```bash
sudo systemctl restart sshd
```

***

## Disabling Root Login over SSH for Security

Prevent root login over SSH to enhance security. Root is the superuser on a Linux system, and allowing remote root logins can be a security risk.

#### Editing SSH Configuration

Edit `/etc/ssh/sshd_config` and set `PermitRootLogin no`.

**Example:**

```bash
PermitRootLogin no
```

This configuration ensures that root login is not permitted over SSH, forcing users to log in with a normal user account and then escalate privileges using `sudo`.

Restart SSH service to apply changes:

```bash
sudo systemctl restart sshd
```

***

## Secure Remote Access with OpenVPN

**OpenVPN** is an open-source VPN protocol that uses custom security protocols to provide secure point-to-point or site-to-site connections. It can traverse firewalls and network address translators (NATs).

#### Installing OpenVPN

**Debian/Ubuntu:**

```bash
sudo apt install openvpn
```

**Arch Linux:**

```bash
sudo pacman -S openvpn
```

**CentOS/Red Hat:**

```bash
sudo yum install openvpn
# or
sudo dnf install openvpn
```

#### Configuring OpenVPN

Generate server and client certificates using Easy-RSA, a small RSA key management package based on OpenSSL.

**Install Easy-RSA:**

```bash
sudo apt install easy-rsa  # Debian/Ubuntu
sudo pacman -S easy-rsa    # Arch Linux
sudo yum install easy-rsa  # CentOS/Red Hat
```

**Initialize Easy-RSA:**

```bash
make-cadir ~/openvpn-ca
cd ~/openvpn-ca
source vars
./clean-all
./build-ca
./build-key-server server
./build-dh
./build-key client1
```

* `make-cadir ~/openvpn-ca`: Creates a new directory for Easy-RSA.
* `source vars`: Sets up environment variables for Easy-RSA.
* `./clean-all`: Removes any previous keys and certificates.
* `./build-ca`: Builds the Certificate Authority (CA) certificate.
* `./build-key-server server`: Builds the server key and certificate.
* `./build-dh`: Generates Diffie-Hellman parameters for key exchange.
* `./build-key client1`: Builds the client key and certificate.

**Configure the server:**

Create a configuration file:

```bash
sudo cp /usr/share/doc/openvpn/examples/sample-config-files/server.conf /etc/openvpn/
```

Edit `/etc/openvpn/server.conf` to match your network settings:

```bash
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
key server.key
dh dh2048.pem
```

* `port 1194`: Specifies the port OpenVPN will listen on.
* `proto udp`: Specifies the protocol to use (UDP is generally preferred for VPNs).
* `dev tun`: Specifies the use of a TUN device (virtual network interface).
* `ca ca.crt`: Specifies the CA certificate.
* `cert server.crt`: Specifies the server certificate.
* `key server.key`: Specifies the server key.
* `dh dh2048.pem`: Specifies the Diffie-Hellman parameters.

**Start and enable OpenVPN service:**

**All distributions:**

```bash
sudo systemctl start openvpn@server
sudo systemctl enable openvpn@server
```

#### Client Configuration

Create a client configuration file:

```bash
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

* `remote your_server_ip 1194`: Specifies the server's IP address and port.
* `ca ca.crt`: Specifies the CA certificate.
* `cert client1.crt`: Specifies the client certificate.
* `key client1.key`: Specifies the client key.
* `remote-cert-tls server`: Ensures the server certificate is signed by the CA.

Transfer the necessary files

to the client:

```bash
scp /etc/openvpn/ca.crt /etc/openvpn/client1.crt /etc/openvpn/client1.key username@client_ip:/etc/openvpn/
```

Start the OpenVPN client:

```bash
sudo openvpn --config /etc/openvpn/client.conf
```

***

## IPsec Configuration for Network Security

**IPsec (Internet Protocol Security)** provides secure IP communications by authenticating and encrypting each IP packet of a communication session.

#### Installing StrongSwan

**Debian/Ubuntu:**

```bash
sudo apt install strongswan
```

**Arch Linux:**

```bash
sudo pacman -S strongswan
```

**CentOS/Red Hat:**

```bash
sudo yum install strongswan
# or
sudo dnf install strongswan
```

#### Basic Configuration

Edit the StrongSwan configuration file `/etc/ipsec.conf`:

```bash
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

* `charondebug="ike 2, knl 2, cfg 2"`: Enables debugging information for IKE, kernel, and configuration.
* `keyexchange=ikev2`: Specifies IKEv2 as the key exchange protocol.
* `authby=secret`: Uses pre-shared secrets for authentication.
* `type=tunnel`: Specifies a tunnel mode connection.
* `dpdaction=clear`: Clears the connection if the Dead Peer Detection (DPD) check fails.
* `left=%any`: Specifies that any local IP address can be used.
* `leftid=@myvpnserver`: Specifies the left (local) identity.
* `leftcert=serverCert.pem`: Specifies the server certificate.
* `leftsendcert=always`: Always sends the certificate.
* `leftsubnet=0.0.0.0/0`: Specifies the local subnet.
* `right=%any`: Specifies that any remote IP address can be used.
* `rightid=@myvpnclient`: Specifies the right (remote) identity.
* `rightauth=eap-mschapv2`: Uses EAP-MSCHAPv2 for authentication.
* `rightdns=8.8.8.8,8.8.4.4`: Specifies the DNS servers.
* `rightsourceip=10.0.0.0/24`: Specifies the IP address pool for clients.
* `auto=add`: Adds the connection automatically.

Edit the authentication file `/etc/ipsec.secrets`:

```bash
: RSA serverKey.pem
myvpnclient : EAP "clientpassword"
```

* `: RSA serverKey.pem`: Specifies the server key.
* `myvpnclient : EAP "clientpassword"`: Specifies the client authentication method and password.

Start and enable StrongSwan service:

```bash
sudo systemctl start strongswan
sudo systemctl enable strongswan
```

***

## Setting Up a Tor Relay or Bridge

**Tor (The Onion Router)** helps you maintain privacy and security on the internet by directing traffic through a free, worldwide, volunteer overlay network consisting of more than seven thousand relays.

#### Installing Tor

**Debian/Ubuntu:**

```bash
sudo apt install tor
```

**Arch Linux:**

```bash
sudo pacman -S tor
```

**CentOS/Red Hat:**

```bash
sudo yum install tor
# or
sudo dnf install tor
```

#### Configuring Tor Relay

Edit the Tor configuration file `/etc/tor/torrc`:

```bash
RunAsDaemon 1
ORPort 9001
DirPort 9030
ExitPolicy reject *:*
SocksPort 0
Log notice file /var/log/tor/notices.log
Nickname your_nickname
ContactInfo your_email@example.com
```

* `RunAsDaemon 1`: Runs Tor as a daemon.
* `ORPort 9001`: Specifies the port for accepting connections from Tor clients.
* `DirPort 9030`: Specifies the directory port.
* `ExitPolicy reject *:*`: Denies all exit traffic.
* `SocksPort 0`: Disables the SOCKS port.
* `Log notice file /var/log/tor/notices.log`: Specifies the log file.
* `Nickname your_nickname`: Sets the relay's nickname.
* `ContactInfo your_email@example.com`: Sets the contact information for the relay operator.

Start and enable Tor service:

```bash
sudo systemctl start tor
sudo systemctl enable tor
```

***

## Using Tor for Anonymous Browsing

**Tor Browser** allows you to browse the internet anonymously by routing your traffic through the Tor network.

#### Installing Tor Browser

**Debian/Ubuntu:**

```bash
sudo add-apt-repository ppa:micahflee/ppa
sudo apt update
sudo apt install torbrowser-launcher
```

**Arch Linux:**

```bash
sudo pacman -S torbrowser-launcher
```

**CentOS/Red Hat:**

```bash
sudo yum install torbrowser-launcher
# or
sudo dnf install torbrowser-launcher
```

#### Launching Tor Browser

**All distributions:**

```bash
torbrowser-launcher
```

Tor Browser bundles Tor with a modified version of the Firefox browser, providing a secure and private browsing experience out-of-the-box.

***
