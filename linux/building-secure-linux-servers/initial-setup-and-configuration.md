# Initial Setup and Configuration

## Table of Contents

1. [Introduction](initial-setup-and-configuration.md#introduction)
2. [Selecting a Secure Linux Distro for Your Server](initial-setup-and-configuration.md#selecting-a-secure-linux-distro-for-your-server)
3. [Initial Linux Server Setup: Steps and Best Practices](initial-setup-and-configuration.md#initial-linux-server-setup-steps-and-best-practices)
4. [Setting Up a Linux Bastion Host](initial-setup-and-configuration.md#setting-up-a-linux-bastion-host)
5. [Infrastructure as Code (IaC) with Terraform](initial-setup-and-configuration.md#infrastructure-as-code-iac-with-terraform)
6. [Using Ansible for Secure Configuration Management](initial-setup-and-configuration.md#using-ansible-for-secure-configuration-management)

***

## Cheat Sheet

**Update and Upgrade the System**

| Distribution   | Command                                      |
| -------------- | -------------------------------------------- |
| Debian/Ubuntu  | `sudo apt update && sudo apt upgrade -y`     |
| Arch Linux     | `sudo pacman -Syu`                           |
| CentOS/Red Hat | `sudo yum update -y` or `sudo dnf update -y` |

**Install Essential Packages**

| Distribution   | Command                                      |
| -------------- | -------------------------------------------- |
| Debian/Ubuntu  | `sudo apt install vim git curl net-tools -y` |
| Arch Linux     | `sudo pacman -S vim git curl net-tools`      |
| CentOS/Red Hat | `sudo yum install vim git curl net-tools -y` |
| CentOS/Red Hat | `sudo dnf install vim git curl net-tools -y` |

**Create a Non-Root User**

| Distribution   | Command                           |
| -------------- | --------------------------------- |
| Debian/Ubuntu  | `sudo adduser username`           |
|                | `sudo usermod -aG sudo username`  |
| Arch Linux     | `sudo useradd -m username`        |
|                | `sudo passwd username`            |
|                | `sudo usermod -aG wheel username` |
| CentOS/Red Hat | `sudo useradd -m username`        |
|                | `sudo passwd username`            |
|                | `sudo usermod -aG wheel username` |

**Secure SSH Access**

<table><thead><tr><th width="310">Distribution</th><th>Command</th></tr></thead><tbody><tr><td>All</td><td><code>sudo vim /etc/ssh/sshd_config</code></td></tr><tr><td></td><td>Change <code>Port</code> and <code>PermitRootLogin</code> settings</td></tr><tr><td>All</td><td><code>sudo systemctl restart ssh</code></td></tr></tbody></table>

***

## Introduction

Setting up a secure Linux server requires careful planning and execution. This chapter guides you through the initial setup and configuration processes, ensuring a strong security foundation for your server. We'll cover choosing a secure Linux distribution, performing essential system updates, creating non-root user accounts, securing SSH access, setting up a Bastion Host, and using tools like Terraform and Ansible for infrastructure management.

***

### Selecting a Secure Linux Distro for Your Server

Choosing the right Linux distribution is the first step in building a secure server. Here are some of the best options:

* **Debian**: Known for its stability and extensive package repository.
* **Ubuntu**: Popular, user-friendly, and has a large support community.
* **Arch Linux**: Offers flexibility and control with a rolling release model.
* **CentOS**: Preferred for enterprise environments due to long-term support.
* **Red Hat**: Enterprise-focused with strong support and security features.

Each of these distributions has its strengths and is well-suited for different scenarios. For enterprise environments, CentOS and Red Hat are often preferred, while Debian and Ubuntu are great for general purposes. Arch Linux is ideal for users who want more control and customization.

***

## Initial Linux Server Setup: Steps and Best Practices

**1. Update and Upgrade the System**

Keeping your system up to date is crucial for security. Use the following commands for different distributions:

*   **Debian/Ubuntu**:

    ```sh
    sudo apt update && sudo apt upgrade -y
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -Syu
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum update -y
    ```

    or

    ```sh
    sudo dnf update -y
    ```

Regularly updating your system ensures that you have the latest security patches and features.

**2. Install Essential Packages**

Install necessary packages for server operation. These packages might include editors, network tools, and version control systems.

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install vim git curl net-tools -y
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S vim git curl net-tools
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install vim git curl net-tools -y
    ```

    or

    ```sh
    sudo dnf install vim git curl net-tools -y
    ```

**3. Create a Non-Root User**

Running services as the root user is risky. Create a new user and assign necessary privileges.

*   **Debian/Ubuntu**:

    ```sh
    sudo adduser username
    sudo usermod -aG sudo username
    ```
*   **Arch Linux**:

    ```sh
    sudo useradd -m username
    sudo passwd username
    sudo usermod -aG wheel username
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo useradd -m username
    sudo passwd username
    sudo usermod -aG wheel username
    ```

**4. Secure SSH Access**

Edit the SSH configuration to disable root login and change the default port.

*   **Debian/Ubuntu/Arch Linux/CentOS/Red Hat**:

    ```sh
    sudo vim /etc/ssh/sshd_config
    ```

    * Change the following lines:

    ```plaintext
    Port 2222
    PermitRootLogin no
    ```

    * Restart the SSH service:

    ```sh
    sudo systemctl restart ssh
    ```

Securing SSH access is vital for protecting your server from unauthorized access.

***

## Setting Up a Linux Bastion Host

A Bastion Host acts as a gateway for accessing other servers in a secure manner.

**1. Install and Configure the Bastion Host**

Install SSH and any necessary tools:

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install openssh-server -y
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S openssh
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install openssh-server -y
    ```

    or

    ```sh
    sudo dnf install openssh-server -y
    ```

**2. Secure SSH Configuration**

Ensure the Bastion Host has a secure SSH configuration (similar to the previous section).

**3. ProxyJump Configuration**

From your local machine, use the Bastion Host to access internal servers:

```sh
ssh -J user@bastion-host user@internal-server
```

Setting up a Bastion Host helps centralize and secure access to your internal servers.

***

## Infrastructure as Code (IaC) with Terraform

**1. Install Terraform**

Follow the installation instructions from the [official Terraform website](https://www.terraform.io/downloads).

**2. Initialize Terraform**

Create a configuration file (`main.tf`) and initialize Terraform:

```sh
terraform init
```

**3. Write Terraform Configuration**

Example `main.tf` for setting up an AWS EC2 instance:

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

**4. Apply the Configuration**

```sh
terraform apply
```

Using Terraform for IaC allows you to automate and manage your infrastructure efficiently.

***

## Using Ansible for Secure Configuration Management

**1. Install Ansible**

Use the package manager specific to your distribution:

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install ansible -y
    ```
*   **Arch Linux**:

    ```sh
    sudo pacman -S ansible
    ```
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install ansible -y
    ```

    or

    ```sh
    sudo dnf install ansible -y
    ```

**2. Create an Ansible Inventory File**

`inventory.ini`:

```ini
[webservers]
web1 ansible_host=192.168.1.101

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

**3. Write a Playbook**

Example playbook `setup.yml`:

```yaml
- hosts: webservers
  become: yes
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present
      when: ansible_os_family == "Debian"

    - name: Ensure Apache is installed
      pacman:
        name: apache
        state: present
      when: ansible_os_family == "Archlinux"

    - name: Ensure Apache is installed
      yum:
        name: httpd
        state: present
      when: ansible_os_family == "RedHat"
```

**4. Run the Playbook**

```sh
ansible-playbook -i inventory.ini setup.yml
```

Using Ansible for configuration management helps automate and ensure consistency across your servers.

***

By following the practical steps and commands provided in this chapter, you can set up and configure your Linux server securely and efficiently. Each section builds on the previous one, creating a comprehensive approach to initial server setup and configuration.
