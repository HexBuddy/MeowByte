# Encryption and Secure Communication

## **Cheat Sheet**

| **Topic**                                 | **Red Hat/CentOS Commands**                                | **Debian/Ubuntu Commands**                                 |
| ----------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| **1. Let's Encrypt for SSL Certificates** | `sudo yum install certbot python2-certbot-apache`          | `sudo apt-get install certbot python3-certbot-apache`      |
|                                           | `sudo certbot --apache -d example.com`                     | `sudo certbot --apache -d example.com`                     |
| **2. SSL/TLS on Apache and Nginx**        | `sudo yum install mod_ssl`                                 | `sudo apt-get install apache2`                             |
|                                           | `sudo systemctl enable httpd`                              | `sudo a2enmod ssl`                                         |
|                                           | `sudo systemctl restart httpd`                             | `sudo systemctl restart apache2`                           |
|                                           |                                                            | `sudo apt-get install nginx`                               |
|                                           |                                                            | `sudo systemctl enable nginx`                              |
|                                           |                                                            | `sudo systemctl restart nginx`                             |
| **3. Enabling HTTP/2**                    | `sudo yum install mod_http2`                               | `sudo apt-get install libapache2-mod-http2`                |
| **4. Encrypting Files with GPG**          | `sudo yum install gnupg2`                                  | `sudo apt-get install gnupg`                               |
|                                           | `gpg --encrypt --recipient recipient@example.com file.txt` | `gpg --encrypt --recipient recipient@example.com file.txt` |
| **5. Full Disk Encryption with LUKS**     | `sudo yum install cryptsetup`                              | `sudo apt-get install cryptsetup`                          |
|                                           | `sudo cryptsetup luksFormat /dev/sdX`                      | `sudo cryptsetup luksFormat /dev/sdX`                      |
|                                           | `sudo cryptsetup open --type luks /dev/sdX mapped_name`    | `sudo cryptsetup open --type luks /dev/sdX mapped_name`    |
| **6. Setting Up OpenVPN Server**          | `sudo yum install openvpn`                                 | `sudo apt-get install openvpn`                             |
|                                           |                                                            |                                                            |
| **7. Database Encryption Techniques**     | Transparent Data Encryption (TDE)                          | Transparent Data Encryption (TDE)                          |
|                                           | Column-level Encryption                                    | Column-level Encryption                                    |
| **8. Hardening Linux Kernel**             | Edit `/etc/sysctl.conf` and apply with `sudo sysctl -p`    | Edit `/etc/sysctl.conf` and apply with `sudo sysctl -p`    |

***

**1. Installing and Using Let's Encrypt for SSL Certificates**

Let's Encrypt provides free SSL/TLS certificates, making it easy to secure websites.

*   **Red Hat/CentOS:**

    ```bash
    sudo yum install certbot python2-certbot-apache
    ```
*   **Debian/Ubuntu:**

    ```bash
    sudo apt-get install certbot python3-certbot-apache
    ```
*   **Obtain SSL Certificate:**

    ```bash
    sudo certbot --apache -d example.com
    ```

    Replace `example.com` with your domain. Certbot will automatically configure Apache/Nginx to use SSL.

**2. Configuring SSL/TLS on Apache and Nginx**

SSL/TLS encryption secures web traffic between clients and servers.

*   **Apache (Red Hat/CentOS):**

    ```bash
    sudo yum install mod_ssl
    sudo systemctl enable httpd
    sudo systemctl restart httpd
    ```
*   **Apache (Debian/Ubuntu):**

    ```bash
    sudo apt-get install apache2
    sudo a2enmod ssl
    sudo systemctl restart apache2
    ```
*   **Nginx (Both):**

    ```bash
    sudo apt-get install nginx
    sudo systemctl enable nginx
    sudo systemctl restart nginx
    ```

**3. Enabling HTTP/2 for Security and Performance**

HTTP/2 improves website performance and security by optimizing protocol overhead.

*   **Apache (Red Hat/CentOS):**

    ```bash
    sudo yum install mod_http2
    ```
*   **Apache (Debian/Ubuntu):**

    ```bash
    sudo apt-get install libapache2-mod-http2
    ```
*   **Nginx (Both):**

    HTTP/2 is enabled by default when supported.

**4. Encrypting Files with GPG**

GPG (GNU Privacy Guard) encrypts files using asymmetric encryption.

*   **Install GPG:**

    ```bash
    sudo yum install gnupg2      # Red Hat/CentOS
    sudo apt-get install gnupg   # Debian/Ubuntu
    ```
*   **Encrypt a File:**

    ```bash
    gpg --encrypt --recipient recipient@example.com file.txt
    ```

**5. Implementing Full Disk Encryption with LUKS**

LUKS (Linux Unified Key Setup) encrypts entire disk partitions.

*   **Install Cryptsetup:**

    ```bash
    sudo yum install cryptsetup      # Red Hat/CentOS
    sudo apt-get install cryptsetup  # Debian/Ubuntu
    ```
*   **Encrypt a Partition:**

    ```bash
    sudo cryptsetup luksFormat /dev/sdX
    sudo cryptsetup open --type luks /dev/sdX mapped_name
    ```

    Replace `/dev/sdX` with the disk/partition you want to encrypt.

**6. Setting Up a Secure OpenVPN Server**

OpenVPN provides secure remote access to private networks.

*   **Install OpenVPN:**

    ```bash
    sudo yum install openvpn       # Red Hat/CentOS
    sudo apt-get install openvpn   # Debian/Ubuntu
    ```
*   **Configure OpenVPN Server:**

    Example configuration in `/etc/openvpn/server.conf`.

**7. Database Encryption Techniques**

Encrypt databases to protect sensitive data.

*   **Transparent Data Encryption (TDE):**

    Encrypts database files and backups at the storage level.
*   **Column-level Encryption:**

    Encrypts specific columns containing sensitive data.

**8. Hardening the Linux Kernel: sysctl and More**

Configure kernel parameters for improved security.

*   **Set Secure sysctl Parameters:**

    Edit `/etc/sysctl.conf` and apply changes with `sudo sysctl -p`.

***
