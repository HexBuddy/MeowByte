# User and Access Management

## Table of Contents

1. [Introduction](user-and-access-management.md#introduction)
2. [Creating and Managing Secure User Accounts](user-and-access-management.md#creating-and-managing-secure-user-accounts)
3. [Implementing Strong Password Policies with PAM](user-and-access-management.md#implementing-strong-password-policies-with-pam)
4. [Configuring PAM for Pluggable Authentication Modules](user-and-access-management.md#configuring-pam-for-pluggable-authentication-modules)
5. [Implementing 2FA for Linux Logins](user-and-access-management.md#implementing-2fa-for-linux-logins)
6. [Setting Up TOTP for Two-Factor Authentication](user-and-access-management.md#setting-up-totp-for-two-factor-authentication)
7. [Single Sign-On (SSO) with SAML](user-and-access-management.md#single-sign-on-sso-with-saml)
8. [Network Authentication with Kerberos](user-and-access-management.md#network-authentication-with-kerberos)
9. [Setting Up a Secure LDAP Server](user-and-access-management.md#setting-up-a-secure-ldap-server)
10. [RADIUS Configuration for Network Authentication](user-and-access-management.md#radius-configuration-for-network-authentication)
11. [Network Access Control (NAC) Implementation](user-and-access-management.md#network-access-control-nac-implementation)

#### **Cheat Sheet**

| **Task**                                     | **Command (Debian/Ubuntu)**                                                                                                | **Command (Arch Linux)**                                                                                                   | **Command (CentOS/Red Hat)**                                                                                               |
| -------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Add a New User                               | `sudo adduser username`                                                                                                    | `sudo useradd -m username`                                                                                                 | `sudo useradd -m username`                                                                                                 |
| Modify User                                  | `sudo usermod -c "comment" username`                                                                                       | `sudo usermod -c "comment" username`                                                                                       | `sudo usermod -c "comment" username`                                                                                       |
| Delete User                                  | `sudo deluser username`                                                                                                    | `sudo userdel username`                                                                                                    | `sudo userdel username`                                                                                                    |
| Set Password Policy with PAM                 | Edit `/etc/pam.d/common-password`, add `password requisite pam_pwquality.so retry=3`                                       | Edit `/etc/security/pwquality.conf`, add `minlen=12`                                                                       | Edit `/etc/security/pwquality.conf`, add `minlen=12`                                                                       |
| Configure TOTP                               | `sudo apt install libpam-google-authenticator`                                                                             | `sudo pacman -S google-authenticator-libpam`                                                                               | `sudo yum install google-authenticator` or `sudo dnf install google-authenticator`                                         |
| Configure Kerberos                           | `sudo apt install krb5-user`                                                                                               | `sudo pacman -S krb5`                                                                                                      | `sudo yum install krb5-server krb5-libs` or `sudo dnf install krb5-server krb5-libs`                                       |
| Install OpenLDAP Server                      | `sudo apt install slapd ldap-utils`                                                                                        | `sudo pacman -S openldap`                                                                                                  | `sudo yum install openldap-servers openldap-clients` or `sudo dnf install openldap-servers openldap-clients`               |
| Install FreeRADIUS Server                    | `sudo apt install freeradius`                                                                                              | `N/A`                                                                                                                      | `sudo yum install freeradius` or `sudo dnf install freeradius`                                                             |
| Allow SSH from Specific IP Ranges (iptables) | `sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j ACCEPT && sudo iptables -A INPUT -p tcp --dport 22 -j DROP` | `sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j ACCEPT && sudo iptables -A INPUT -p tcp --dport 22 -j DROP` | `sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j ACCEPT && sudo iptables -A INPUT -p tcp --dport 22 -j DROP` |
| Block Specific MAC Address (iptables)        | `sudo iptables -A INPUT -m mac --mac-source 00:11:22:33:44:55 -j DROP`                                                     | `sudo iptables -A INPUT -m mac --mac-source 00:11:22:33:44:55 -j DROP`                                                     | `sudo iptables -A INPUT -m mac --mac-source 00:11:22:33:44:55 -j DROP`                                                     |
| Save iptables Rules                          | \`sudo iptables-save                                                                                                       | sudo tee /etc/iptables/rules.v4\`                                                                                          | `sudo iptables-save > /etc/iptables/iptables.rules`                                                                        |
| Apply iptables Rules                         | `sudo iptables-restore < /etc/iptables/rules.v4`                                                                           | `sudo iptables-restore < /etc/iptables/iptables.rules`                                                                     | `sudo iptables-restore < /etc/sysconfig/iptables`                                                                          |

***

***

## Introduction

Managing user access and authentication is critical for maintaining a secure Linux environment. This chapter delves into creating and managing user accounts, implementing robust password policies, configuring Pluggable Authentication Modules (PAM), setting up Two-Factor Authentication (2FA), and more. We also cover advanced topics such as Single Sign-On (SSO), Kerberos, LDAP, RADIUS, and Network Access Control (NAC) to provide comprehensive security for your Linux server.

***

## Creating and Managing Secure User Accounts

Creating and managing user accounts with the least privileges necessary is a foundational security practice. This section covers the commands and best practices for various Linux distributions.

**Creating a New User**

*   **Debian/Ubuntu**:

    ```sh
    sudo adduser username
    ```
*   **Arch Linux**:

    ```sh
    sudo useradd -m username
    sudo passwd username
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo useradd -m username
    sudo passwd username
    ```

**Granting Sudo Privileges**

*   **Debian/Ubuntu**:

    ```sh
    sudo usermod -aG sudo username
    ```
*   **Arch Linux**:

    ```sh
    sudo usermod -aG wheel username
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo usermod -aG wheel username
    ```

**Removing a User**

*   **All**:

    ```sh
    sudo deluser username
    sudo rm -rf /home/username
    ```

**Best Practices**

1. **Least Privilege Principle**: Only grant users the permissions they need to perform their tasks.
2. **Regular Audits**: Periodically review user accounts and their permissions.
3. **Strong Passwords**: Enforce strong password policies (covered in the next section).

***

## Implementing Strong Password Policies with PAM

The Pluggable Authentication Module (PAM) framework is essential for managing authentication policies, including enforcing strong password rules.

**Configuring PAM for Strong Passwords**

Edit the PAM configuration file `/etc/pam.d/common-password` (Debian/Ubuntu) or `/etc/pam.d/system-auth` (CentOS/Red Hat):

```sh
sudo vim /etc/pam.d/common-password
```

Add the following lines to enforce password complexity:

```plaintext
password requisite pam_pwquality.so retry=3 minlen=12 dcredit=-1 ucredit=-1 ocredit=-1 lcredit=-1
```

**Parameters Explanation**

* `retry=3`: Number of retry attempts allowed for setting a new password.
* `minlen=12`: Minimum password length.
* `dcredit=-1`: Require at least one digit.
* `ucredit=-1`: Require at least one uppercase letter.
* `ocredit=-1`: Require at least one special character.
* `lcredit=-1`: Require at least one lowercase letter.

**Installing `pam_pwquality`**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install libpam-pwquality
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S pam
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install pam_pwquality
    ```

    or

    ```sh
    sudo dnf install pam_pwquality
    ```

***

## Configuring PAM for Pluggable Authentication Modules

PAM allows for flexible and modular authentication management. It can be configured for various authentication mechanisms and policies.

**Common PAM Configuration Files**

* `/etc/pam.d/login`: Controls login behavior.
* `/etc/pam.d/sshd`: Controls SSH login behavior.
* `/etc/pam.d/sudo`: Controls sudo command behavior.

**Example: Requiring Password for `sudo`**

Edit `/etc/pam.d/sudo`:

```sh
sudo vim /etc/pam.d/sudo
```

Add the following line to ensure sudo prompts for a password:

```plaintext
auth required pam_unix.so
```

**Example: Limiting Access to Specific Times**

Edit `/etc/security/time.conf`:

```sh
sudo vim /etc/security/time.conf
```

Add rules to restrict login times, e.g., allow logins only during work hours:

```plaintext
login ; * ; * ; Al0800-1800
```

***

## Implementing 2FA for Linux Logins

Two-Factor Authentication (2FA) adds an extra layer of security to user logins.

**Installing Google Authenticator**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install libpam-google-authenticator
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S google-authenticator-libpam
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install google-authenticator
    ```

    or

    ```sh
    sudo dnf install google-authenticator
    ```

**Configuring Google Authenticator**

Run the following command for each user to set up 2FA:

```sh
google-authenticator
```

Answer the prompts to configure 2FA. Edit `/etc/pam.d/sshd` and add:

```plaintext
auth required pam_google_authenticator.so
```

Edit `/etc/ssh/sshd_config` to enable 2FA for SSH:

```plaintext
ChallengeResponseAuthentication yes
```

Restart SSH:

```sh
sudo systemctl restart ssh
```

***

## Setting Up TOTP for Two-Factor Authentication

Time-Based One-Time Password (TOTP) is another form of 2FA.

**Installing and Configuring `oathtool`**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install oathtool
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S oathtool
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install oathtool
    ```

    or

    ```sh
    sudo dnf install oathtool
    ```

Generate a TOTP secret:

```sh
oathtool --totp -b "YourSecretKey"
```

Integrate with PAM by editing `/etc/pam.d/sshd`:

```plaintext
auth required pam_oath.so usersfile=/etc/users.oath window=10 digits=6
```

Add user credentials to `/etc/users.oath`:

```plaintext
HOTP/T30/6 username - YourSecretKey
```

Restart SSH:

```sh
sudo systemctl restart ssh
```

***

## Single Sign-On (SSO) with SAML

Single Sign-On (SSO) allows users to log in with a single set of credentials across multiple systems.

**Setting Up SAML with SimpleSAMLphp**

1. **Install SimpleSAMLphp**:

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install simplesamlphp
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install simplesamlphp
    ```

    or

    ```sh
    sudo dnf install simplesamlphp
    ```

2. **Configure SimpleSAMLphp**:
   * Edit `config/config.php` to set up basic configuration.
   * Configure authentication sources in `config/authsources.php`.
3. **Integrate with Applications**:
   * Follow the SimpleSAMLphp documentation to integrate SAML authentication with your web applications.

SSO simplifies user management and improves security by reducing the number of credentials users need to manage.

***

## Network Authentication with Kerberos

Kerberos provides strong authentication for client-server applications.

**Installing Kerberos**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install krb5-kdc krb5-admin-server
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S krb5
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install krb5-server krb5-workstation
    ```

    or

    ```sh
    sudo dnf install krb5-server krb5-workstation
    ```

**Configuring Kerberos**

1. **Edit Kerberos Configuration File**:
   *   `/etc/krb5.conf`:

       ```plaintext
       [libdefaults]
           default_realm = EXAMPLE.COM

       [realms]
           EXAMPLE.COM = {
               kdc = kdc.example.com
               admin_server = admin.example.com
           }

       [domain_realm]
           .example.com = EXAMPLE.COM
           example.com = EXAMPLE.COM
       ```
2.  **Create the Kerberos Database**:

    ```sh
    sudo kdb5_util create -s
    ```
3.  **Add Administrators**:

    ```sh
    sudo kadmin.local
    kadmin.local: addprinc admin/admin
    kadmin.local: quit
    ```
4.  **Start Kerberos Services**:

    ```sh
    sudo systemctl start krb5-kdc
    sudo systemctl start kr
    ```

b5-admin-server

````

#### Authenticating Users with Kerberos

- **Client Configuration**: Ensure the `/etc/krb5.conf` file is correctly configured on client machines.
- **Obtaining a Ticket**:
```sh
kinit username
````

Kerberos improves security by using encrypted tickets for authentication.

***

## Setting Up a Secure LDAP Server

Lightweight Directory Access Protocol (LDAP) is widely used for centralized authentication and directory services.

**Installing OpenLDAP**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install slapd ldap-utils
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S openldap
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install openldap-servers openldap-clients
    ```

    or

    ```sh
    sudo dnf install openldap-servers openldap-clients
    ```

**Configuring OpenLDAP**

1. **Configure the LDAP Server**:
   *   Initialize the LDAP database:

       ```sh
       sudo dpkg-reconfigure slapd
       ```
   * Follow the prompts to set the domain, organization name, and admin password.
2. **Add LDAP Entries**:
   *   Create a file `base.ldif`:

       ```plaintext
       dn: ou=users,dc=example,dc=com
       objectClass: organizationalUnit
       ou: users

       dn: cn=admin,dc=example,dc=com
       objectClass: organizationalRole
       cn: admin
       description: LDAP administrator
       ```
   *   Add the entries to LDAP:

       ```sh
       sudo ldapadd -x -D cn=admin,dc=example,dc=com -W -f base.ldif
       ```
3. **Configure LDAP Clients**:
   *   Install LDAP client utilities:

       ```sh
       sudo apt install libnss-ldap libpam-ldap ldap-utils
       ```
   * Follow the configuration prompts to set up the LDAP client.

LDAP provides centralized authentication, simplifying user management across multiple systems.

***

## RADIUS Configuration for Network Authentication

Remote Authentication Dial-In User Service (RADIUS) is used for remote user authentication and accounting.

**Installing FreeRADIUS**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install freeradius
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install freeradius
    ```

    or

    ```sh
    sudo dnf install freeradius
    ```

**Configuring FreeRADIUS**

1. **Edit the Main Configuration File**:
   *   `/etc/freeradius/3.0/radiusd.conf`:

       ```plaintext
       prefix = /usr
       exec_prefix = ${prefix}
       sysconfdir = ${prefix}/etc
       localstatedir = /var
       sbindir = ${exec_prefix}/sbin
       logdir = ${localstatedir}/log/radius
       raddbdir = ${sysconfdir}/raddb
       radacctdir = ${logdir}/radacct
       ```
2. **Set Up Clients and Users**:
   *   `/etc/freeradius/3.0/clients.conf`:

       ```plaintext
       client localhost {
           ipaddr = 127.0.0.1
           secret = testing123
           require_message_authenticator = no
           nas_type = other
       }
       ```
   *   `/etc/freeradius/3.0/mods-config/files/authorize`:

       ```plaintext
       testing Cleartext-Password := "password"
       ```
3.  **Start the FreeRADIUS Service**:

    ```sh
    sudo systemctl start freeradius
    ```

FreeRADIUS supports various authentication methods and can be integrated with LDAP, Kerberos, and other services.

***

## Network Access Control (NAC) Implementation

Network Access Control (NAC) ensures that only authorized and compliant devices can access the network.

**Implementing NAC with `iptables`**

1. **Define NAC Rules**:
   *   Allow SSH from specific IP ranges:

       ```sh
       sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j ACCEPT
       sudo iptables -A INPUT -p tcp --dport 22 -j DROP
       ```
2. **Create NAC Policies**:
   *   Block non-compliant devices:

       ```sh
       sudo iptables -A INPUT -m mac --mac-source 00:11:22:33:44:55 -j DROP
       ```
3. **Save and Apply Rules**:
   *   Save the rules:

       ```sh
       sudo iptables-save | sudo tee /etc/iptables/rules.v4
       ```
   *   Apply the rules:

       ```sh
       sudo iptables-restore < /etc/iptables/rules.v4
       ```

NAC policies help ensure that only authorized and secure devices can access the network.

***
