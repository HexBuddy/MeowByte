# User and Access Management

Managing user accounts and access is critical for securing a Linux server. This section covers various aspects of user and access management across different Linux distributions: Debian, Ubuntu, Arch Linux, CentOS, and Red Hat.

## Cheat Sheet

#### User and Access Management Commands

**General User Management**

| **Operation**           | **Debian/Ubuntu**                         | **CentOS/Red Hat**                        | **Arch Linux**                            |
| ----------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| **Create a new user**   | `sudo adduser <username>`                 | `sudo useradd <username>`                 | `sudo useradd <username>`                 |
| **Delete a user**       | `sudo deluser <username>`                 | `sudo userdel <username>`                 | `sudo userdel <username>`                 |
| **Add user to a group** | `sudo usermod -aG <groupname> <username>` | `sudo usermod -aG <groupname> <username>` | `sudo usermod -aG <groupname> <username>` |

**Password Management**

| **Operation**                           | **Command**                  |
| --------------------------------------- | ---------------------------- |
| **Change a user’s password**            | `sudo passwd <username>`     |
| **Force password change on next login** | `sudo chage -d 0 <username>` |

**Password Policies with PAM**

| **Operation**                   | **Debian/Ubuntu**                                       | **CentOS/Red Hat**                                      | **Arch Linux**                                          |
| ------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| **Edit PAM configuration file** | `/etc/pam.d/common-password`                            | `/etc/pam.d/system-auth`                                | `/etc/pam.d/system-login`                               |
| **Set password length**         | `password requisite pam_pwquality.so retry=3 minlen=12` | `password requisite pam_pwquality.so retry=3 minlen=12` | `password requisite pam_pwquality.so retry=3 minlen=12` |

**Two-Factor Authentication (2FA)**

| **Operation**                      | **Debian/Ubuntu**                                  | **CentOS/Red Hat**                      | **Arch Linux**                               |
| ---------------------------------- | -------------------------------------------------- | --------------------------------------- | -------------------------------------------- |
| **Install Google Authenticator**   | `sudo apt-get install libpam-google-authenticator` | `sudo yum install google-authenticator` | `sudo pacman -S libpam-google-authenticator` |
| **Configure Google Authenticator** | `google-authenticator`                             | `google-authenticator`                  | `google-authenticator`                       |

## **Creating and Managing Secure User Accounts**

Creating and managing user accounts is a fundamental aspect of server administration. Here are the steps for various distributions:

*   **Debian/Ubuntu**:

    ```sh
    sudo adduser <username>
    sudo passwd <username>  # Set password for the new user
    sudo usermod -aG <groupname> <username>  # Add user to a group
    ```
*   **CentOS/Red Hat/Arch**:

    ```sh
    sudo useradd <username>
    sudo passwd <username>  # Set password for the new user
    sudo usermod -aG <groupname> <username>  # Add user to a group
    ```

To delete a user:

*   **Debian/Ubuntu**:

    ```sh
    sudo deluser <username>
    ```
*   **CentOS/Red Hat/Arch**:

    ```sh
    sudo userdel <username>
    ```

## **Implementing Strong Password Policies with PAM**

PAM (Pluggable Authentication Modules) is used to enforce strong password policies. Here’s how to set it up:

* **Edit the PAM configuration file**:
  * **Debian/Ubuntu**: `/etc/pam.d/common-password`
  * **CentOS/Red Hat**: `/etc/pam.d/system-auth`
  * **Arch Linux**: `/etc/pam.d/system-login`
*   **Set password length**:

    ```sh
    password requisite pam_pwquality.so retry=3 minlen=12
    ```

This line enforces a minimum password length of 12 characters and allows three attempts for the user to enter a password.

**Example Configuration**:

In `/etc/pam.d/common-password` for Debian/Ubuntu:

```sh
password requisite pam_pwquality.so retry=3 minlen=12 difok=3
```

In `/etc/pam.d/system-auth` for CentOS/Red Hat:

```sh
password requisite pam_pwquality.so retry=3 minlen=12 difok=3
```

In `/etc/pam.d/system-login` for Arch Linux:

```sh
password requisite pam_pwquality.so retry=3 minlen=12 difok=3
```

## **Configuring PAM for Pluggable Authentication Modules**

To configure PAM, you need to edit the PAM configuration files for the specific services. Here are some examples:

* **Password policy configuration**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo nano /etc/pam.d/common-password
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo nano /etc/pam.d/system-auth
      ```
  *   **Arch Linux**:

      ```sh
      sudo nano /etc/pam.d/system-login
      ```

In these files, you can add modules like `pam_pwquality` to enforce password policies.

**Example Configuration for SSH**:

Edit `/etc/pam.d/sshd` and add:

```sh
auth required pam_tally2.so deny=5 unlock_time=900
```

This line will lock the user out after 5 failed login attempts and unlock the account after 15 minutes.

## **Implementing 2FA for Linux Logins**

Two-Factor Authentication (2FA) adds an extra layer of security. Google Authenticator is a popular choice.

* **Install Google Authenticator**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo apt-get install libpam-google-authenticator
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo yum install google-authenticator
      ```
  *   **Arch Linux**:

      ```sh
      sudo pacman -S libpam-google-authenticator
      ```
*   **Configure Google Authenticator**:

    ```sh
    google-authenticator
    ```

Follow the prompts to set up 2FA for the user account. You will need to scan a QR code with your mobile device using the Google Authenticator app.

*   **Edit the PAM configuration for SSH**:

    ```sh
    sudo nano /etc/pam.d/sshd
    ```

    Add the following line:

    ```sh
    auth required pam_google_authenticator.so
    ```
*   **Edit the SSH configuration**:

    ```sh
    sudo nano /etc/ssh/sshd_config
    ```

    Add or modify the following lines:

    ```sh
    ChallengeResponseAuthentication yes
    ```

Restart SSH service:

*   **Debian/Ubuntu**:

    ```sh
    sudo systemctl restart ssh
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo systemctl restart sshd
    ```
*   **Arch Linux**:

    ```sh
    sudo systemctl restart sshd
    ```

## **Setting Up TOTP for Two-Factor Authentication**

TOTP (Time-based One-Time Password) is another method for 2FA, which can be set up using Google Authenticator or other TOTP apps.

* **Install required packages**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo apt-get install libpam-google-authenticator
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo yum install google-authenticator
      ```
  *   **Arch Linux**:

      ```sh
      sudo pacman -S libpam-google-authenticator
      ```
*   **Configure Google Authenticator**:

    ```sh
    google-authenticator
    ```

Follow the prompts to complete the setup.

*   **Configure PAM for TOTP**: Edit `/etc/pam.d/sshd` and add:

    ```sh
    auth required pam_google_authenticator.so
    ```

Edit `/etc/ssh/sshd_config` to enable challenge-response authentication:

```sh
ChallengeResponseAuthentication yes
```

Restart SSH service:

*   **Debian/Ubuntu**:

    ```sh
    sudo systemctl restart ssh
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo systemctl restart sshd
    ```
*   **Arch Linux**:

    ```sh
    sudo systemctl restart sshd
    ```

## **Single Sign-On (SSO) with SAML**

Single Sign-On (SSO) using SAML allows users to authenticate once and gain access to multiple systems. This can be set up using various tools and services such as Keycloak or Auth0.

* **Install Keycloak**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo apt-get install keycloak
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo yum install keycloak
      ```
* **Configure Keycloak**: Follow the [Keycloak Documentation](https://www.keycloak.org/docs/latest/server\_installation/).
* **Configure SAML SSO**: Create and configure SAML clients in Keycloak and integrate them with your applications.

## **Network Authentication with Kerberos**

Kerberos is a network authentication protocol that uses secret-key cryptography. Here’s how to set

it up:

* **Install Kerberos**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo apt-get install krb5-kdc krb5-admin-server
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo yum install krb5-server krb5-libs krb5-auth-dialog
      ```
* **Configure Kerberos**:
  * Edit `/etc/krb5.conf` to configure the Kerberos realm and domain.
  *   Initialize the Kerberos database:

      ```sh
      sudo krb5_newrealm
      ```
*   **Add principals (users)**:

    ```sh
    sudo kadmin.local
    kadmin.local: addprinc <username>
    ```
* **Start Kerberos services**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo systemctl start krb5-kdc
      sudo systemctl start krb5-admin-server
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo systemctl start krb5kdc
      sudo systemctl start kadmin
      ```

## **Setting Up a Secure LDAP Server**

LDAP (Lightweight Directory Access Protocol) is used for accessing and managing directory information. OpenLDAP is a common choice.

* **Install OpenLDAP**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo apt-get install slapd ldap-utils
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo yum install openldap openldap-servers openldap-clients
      ```
* **Configure OpenLDAP**:
  *   **Initial setup**:

      ```sh
      sudo dpkg-reconfigure slapd
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo systemctl start slapd
      sudo systemctl enable slapd
      ```
* **Add LDAP entries**:
  *   **Create an LDIF file (e.g., `base.ldif`)**:

      ```ldif
      dn: dc=example,dc=com
      objectClass: top
      objectClass: dcObject
      objectClass: organization
      o: Example Organization
      dc: example
      ```
  *   **Add the entry to the LDAP directory**:

      ```sh
      ldapadd -x -D cn=admin,dc=example,dc=com -W -f base.ldif
      ```

## **RADIUS Configuration for Network Authentication**

RADIUS (Remote Authentication Dial-In User Service) is used for centralized authentication.

* **Install FreeRADIUS**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo apt-get install freeradius
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo yum install freeradius freeradius-utils
      ```
* **Configure FreeRADIUS**:
  *   **Edit configuration files**:

      ```sh
      sudo nano /etc/freeradius/3.0/clients.conf
      sudo nano /etc/freeradius/3.0/users
      ```
  *   **Add a client** in `clients.conf`:

      ```sh
      client localhost {
          ipaddr = 127.0.0.1
          secret = testing123
      }
      ```
  *   **Add a user** in `users`:

      ```sh
      testuser Cleartext-Password := "password"
      ```
* **Start FreeRADIUS**:
  *   **Debian/Ubuntu**:

      ```sh
      sudo systemctl start freeradius
      sudo systemctl enable freeradius
      ```
  *   **CentOS/Red Hat**:

      ```sh
      sudo systemctl start radiusd
      sudo systemctl enable radiusd
      ```

## **Network Access Control (NAC) Implementation**

NAC solutions help to enforce policies for network access control. PacketFence is a popular open-source solution.

* **Install PacketFence**:
  *   **Debian/Ubuntu**:

      ```sh
      wget https://packages.packetfence.org/releases/PacketFence-12.1.0-1.x86_64.deb
      sudo dpkg -i PacketFence-12.1.0-1.x86_64.deb
      sudo apt-get -f install
      ```
  *   **CentOS/Red Hat**:

      ```sh
      wget https://packages.packetfence.org/releases/PacketFence-12.1.0-1.el7.x86_64.rpm
      sudo yum install PacketFence-12.1.0-1.el7.x86_64.rpm
      ```
* **Configure PacketFence**:
  * Follow the [PacketFence Configuration Guide](https://www.packetfence.org/doc.html).

#### Resources

* [PAM Documentation](https://linux-pam.org/Linux-PAM-html/)
* [Google Authenticator PAM Module](https://github.com/google/google-authenticator-libpam)
* [Keycloak Documentation](https://www.keycloak.org/documentation.html)
* [Kerberos Documentation](https://web.mit.edu/kerberos/)
* [OpenLDAP Documentation](https://www.openldap.org/doc/)
* [FreeRADIUS Documentation](https://networkradius.com/doc/)
* [PacketFence Documentation](https://www.packetfence.org/doc.html)

This comprehensive guide ensures you have a practical, step-by-step approach to managing user accounts and access securely on various Linux distributions.
