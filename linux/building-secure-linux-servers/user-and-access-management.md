# User and Access Management

### Table of Contents

* Introduction
* Creating and Managing Secure User Accounts
* Implementing Strong Password Policies with PAM
* Configuring PAM for Pluggable Authentication Modules
* Implementing 2FA for Linux Logins
* Setting Up TOTP for Two-Factor Authentication
* Single Sign-On (SSO) with SAML
* Network Authentication with Kerberos
* Setting Up a Secure LDAP Server
* RADIUS Configuration for Network Authentication
* Network Access Control (NAC) Implementation

## Introduction

Managing user access and authentication is critical for maintaining a secure Linux environment. This chapter delves into creating and managing user accounts, implementing robust password policies, configuring Pluggable Authentication Modules (PAM), setting up Two-Factor Authentication (2FA), and more. We also cover advanced topics such as Single Sign-On (SSO), Kerberos, LDAP, RADIUS, and Network Access Control (NAC) to provide comprehensive security for your Linux server.

## Creating and Managing Secure User Accounts

Creating and managing user accounts with the least privileges necessary is a foundational security practice. This section covers the commands and best practices for various Linux distributions.

#### Creating a New User

**Debian/Ubuntu:**

```bash
sudo adduser username
```

**Arch Linux:**

```bash
sudo useradd -m username
sudo passwd username
```

**CentOS/Red Hat:**

```bash
sudo useradd -m username
sudo passwd username
```

#### Granting Sudo Privileges

**Debian/Ubuntu:**

```bash
sudo usermod -aG sudo username
```

**Arch Linux:**

```bash
sudo usermod -aG wheel username
```

**CentOS/Red Hat:**

```bash
sudo usermod -aG wheel username
```

#### Removing a User

**All:**

```bash
sudo deluser username
sudo rm -rf /home/username
```

#### Best Practices

* **Least Privilege Principle:** Only grant users the permissions they need to perform their tasks.
* **Regular Audits:** Periodically review user accounts and their permissions.
* **Strong Passwords:** Enforce strong password policies (covered in the next section).

## Implementing Strong Password Policies with PAM

The Pluggable Authentication Module (PAM) framework is essential for managing authentication policies, including enforcing strong password rules.

#### Configuring PAM for Strong Passwords

Edit the PAM configuration file `/etc/pam.d/common-password` (Debian/Ubuntu) or `/etc/pam.d/system-auth` (CentOS/Red Hat):

```bash
sudo vim /etc/pam.d/common-password
```

Add the following lines to enforce password complexity:

```
password requisite pam_pwquality.so retry=3 minlen=12 dcredit=-1 ucredit=-1 ocredit=-1 lcredit=-1
```

**Parameters Explanation**

* `retry=3`: Number of retry attempts allowed for setting a new password.
* `minlen=12`: Minimum password length.
* `dcredit=-1`: Require at least one digit.
* `ucredit=-1`: Require at least one uppercase letter.
* `ocredit=-1`: Require at least one special character.
* `lcredit=-1`: Require at least one lowercase letter.

#### Installing `pam_pwquality`

**Debian/Ubuntu:**

```bash
sudo apt install libpam-pwquality
```

**Arch Linux:**

```bash
sudo pacman -S pam
```

**CentOS/Red Hat:**

```bash
sudo yum install pam_pwquality
# or
sudo dnf install pam_pwquality
```

## Configuring PAM for Pluggable Authentication Modules

PAM allows for flexible and modular authentication management. It can be configured for various authentication mechanisms and policies.

#### Common PAM Configuration Files

* `/etc/pam.d/login`: Controls login behavior.
* `/etc/pam.d/sshd`: Controls SSH login behavior.
* `/etc/pam.d/sudo`: Controls sudo command behavior.

#### Example: Requiring Password for `sudo`

Edit `/etc/pam.d/sudo`:

```bash
sudo vim /etc/pam.d/sudo
```

Add the following line to ensure `sudo` prompts for a password:

```
auth required pam_unix.so
```

#### Example: Limiting Access to Specific Times

Edit `/etc/security/time.conf`:

```bash
sudo vim /etc/security/time.conf
```

Add rules to restrict login times, e.g., allow logins only during work hours:

```
login ; * ; * ; Al0800-1800
```

## Implementing 2FA for Linux Logins

Two-Factor Authentication (2FA) adds an extra layer of security to user logins.

#### Installing Google Authenticator

**Debian/Ubuntu:**

```bash
sudo apt install libpam-google-authenticator
```

**Arch Linux:**

```bash
sudo pacman -S google-authenticator-libpam
```

**CentOS/Red Hat:**

```bash
sudo yum install google-authenticator
# or
sudo dnf install google-authenticator
```

#### Configuring Google Authenticator

Run the following command for each user to set up 2FA:

```bash
google-authenticator
```

Answer the prompts to configure 2FA. Edit `/etc/pam.d/sshd` and add:

```
auth required pam_google_authenticator.so
```

Edit `/etc/ssh/sshd_config` to enable 2FA for SSH:

```
ChallengeResponseAuthentication yes
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

## Setting Up TOTP for Two-Factor Authentication

Time-Based One-Time Password (TOTP) is another form of 2FA.

#### Installing and Configuring `oathtool`

**Debian/Ubuntu:**

```bash
sudo apt install oathtool
```

**Arch Linux:**

```bash
sudo pacman -S oathtool
```

**CentOS/Red Hat:**

```bash
sudo yum install oathtool
# or
sudo dnf install oathtool
```

Generate a TOTP secret:

```bash
oathtool --totp -b "YourSecretKey"
```

Integrate with PAM by editing `/etc/pam.d/sshd`:

```
auth required pam_oath.so usersfile=/etc/users.oath window=10 digits=6
```

Add user credentials to `/etc/users.oath`:

```
HOTP/T30/6 username - YourSecretKey
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

## Single Sign-On (SSO) with SAML

Single Sign-On (SSO) allows users to log in with a single set of credentials across multiple systems.

#### Setting Up SAML with SimpleSAMLphp

**Debian/Ubuntu:**

```bash
sudo apt install simplesamlphp
```

**CentOS/Red Hat:**

```bash
sudo yum install simplesamlphp
# or
sudo dnf install simplesamlphp
```

**Configure SimpleSAMLphp:**

1. Edit `config/config.php` to set up basic configuration.
2. Configure authentication sources in `config/authsources.php`.

**Integrate with Applications:**

Follow the SimpleSAMLphp documentation to integrate SAML authentication with your web applications.

SSO simplifies user management and improves security by reducing the number of credentials users need to manage.

## Network Authentication with Kerberos

Kerberos provides strong authentication for client-server applications.

#### Installing Kerberos

**Debian/Ubuntu:**

```bash
sudo apt install krb5-kdc krb5-admin-server
```

**Arch Linux:**

```bash
sudo pacman -S krb5
```

**CentOS/Red Hat:**

```bash
sudo yum install krb5-server krb5-workstation
# or
sudo dnf install krb5-server krb5-workstation
```

#### Configuring Kerberos

Edit Kerberos Configuration File `/etc/krb5.conf`:

```
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

Create the Kerberos Database:

```bash
sudo kdb5_util create -s
```

Add Administrators:

```bash
sudo kadmin.local
kadmin.local: addprinc admin/admin
kadmin.local: quit
```

Start Kerberos Services:

```bash
sudo systemctl start krb5-kdc
sudo systemctl start krb5-admin-server
```

#### Authenticating Users with Kerberos

**Client Configuration:** Ensure the `/etc/krb5.conf` file is correctly configured on client machines.

**Obtaining a Ticket:**

```bash
kinit username
```

Kerberos improves security by using encrypted tickets for authentication.

## Setting Up a Secure LDAP Server

Lightweight Directory Access Protocol (LDAP) is widely used for centralized authentication and directory services.

#### Installing OpenLDAP

**Debian/Ubuntu:**

```bash
sudo apt install slapd ldap-utils
```

**Arch Linux:**

```bash
sudo pacman -S openldap
```

**CentOS/Red Hat:**

```bash
sudo yum install openldap-servers openldap-clients
# or
sudo dnf install openldap-servers openldap-clients
```

#### Configuring OpenLDAP

**Configure the**

LDAP Server:

Initialize the LDAP database:

```bash
sudo dpkg-reconfigure slapd
```

Follow the prompts to set the domain, organization name, and admin password.

**Add LDAP Entries:**

Create a file `base.ldif`:

```
dn: ou=users,dc=example,dc=com
objectClass: organizationalUnit
ou: users

dn: cn=admin,dc=example,dc=com
objectClass: organizationalRole
cn: admin
description: LDAP administrator
```

Add the entries to LDAP:

```bash
sudo ldapadd -x -D cn=admin,dc=example,dc=com -W -f base.ldif
```

**Configure LDAP Clients:**

Install LDAP client utilities:

```bash
sudo apt install libnss-ldap libpam-ldap ldap-utils
```

Follow the configuration prompts to set up the LDAP client.

LDAP provides centralized authentication, simplifying user management across multiple systems.

## RADIUS Configuration for Network Authentication

Remote Authentication Dial-In User Service (RADIUS) is used for remote user authentication and accounting.

#### Installing FreeRADIUS

**Debian/Ubuntu:**

```bash
sudo apt install freeradius
```

**CentOS/Red Hat:**

```bash
sudo yum install freeradius
# or
sudo dnf install freeradius
```

#### Configuring FreeRADIUS

Edit the Main Configuration File `/etc/freeradius/3.0/radiusd.conf`:

```
prefix = /usr
exec_prefix = ${prefix}
sysconfdir = ${prefix}/etc
localstatedir = /var
sbindir = ${exec_prefix}/sbin
logdir = ${localstatedir}/log/radius
raddbdir = ${sysconfdir}/raddb
radacctdir = ${logdir}/radacct
```

**Set Up Clients and Users:**

Edit `/etc/freeradius/3.0/clients.conf`:

```
client localhost {
    ipaddr = 127.0.0.1
    secret = testing123
    require_message_authenticator = no
    nas_type = other
}
```

Edit `/etc/freeradius/3.0/mods-config/files/authorize`:

```
testing Cleartext-Password := "password"
```

Start the FreeRADIUS Service:

```bash
sudo systemctl start freeradius
```

FreeRADIUS supports various authentication methods and can be integrated with LDAP, Kerberos, and other services.

## Network Access Control (NAC) Implementation

Network Access Control (NAC) ensures that only authorized and compliant devices can access the network.

#### Implementing NAC with `iptables`

**Define NAC Rules:**

Allow SSH from specific IP ranges:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
```

**Create NAC Policies:**

Block non-compliant devices:

```bash
sudo iptables -A INPUT -m mac --mac-source 00:11:22:33:44:55 -j DROP
```

**Save and Apply Rules:**

Save the rules:

```bash
sudo iptables-save | sudo tee /etc/iptables/rules.v4
```

Apply the rules:

```bash
sudo iptables-restore < /etc/iptables/rules.v4
```

NAC policies help ensure that only authorized and secure devices can access the network

***

