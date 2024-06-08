# Linux Administration

## Basic Linux Concepts:

1. What is Linux?
   * Linux is a free and open-source operating system kernel that serves as the foundation for various Unix-like operating systems.
2. What is a distribution (distro) in Linux?
   * A Linux distribution is a collection of software based on the Linux kernel and often includes system utilities, libraries, and applications.
3. What is the root user in Linux?
   * The root user, also known as the superuser, has administrative privileges and can perform tasks that regular users cannot, such as modifying system files and installing software.
4. What is the home directory in Linux?
   * The home directory is the default directory for each user and is represented by the tilde (\~) symbol followed by the username.
5. How do you list files and directories in Linux?
   * Use the `ls` command.

## Filesystem Management:

6. What is a filesystem in Linux?
   * A filesystem is a method of organizing and storing files on a computer.
7. How do you navigate directories in Linux?
   * Use the `cd` command followed by the directory name.
8. What is the root directory in Linux?
   * The root directory, represented by `/`, is the top-level directory in the filesystem hierarchy.
9. How do you create a directory in Linux?
   * Use the `mkdir` command followed by the directory name.
10. How do you remove a directory in Linux?
    * Use the `rmdir` command followed by the directory name.

## User and Group Management:

11. How do you create a new user in Linux?
    * Use the `useradd` command followed by the username.
12. How do you change a user's password in Linux?
    * Use the `passwd` command followed by the username.
13. How do you add a user to a group in Linux?
    * Use the `usermod` command with the `-aG` option followed by the group name and username.
14. What is the purpose of the `sudo` command?
    * The `sudo` command allows a permitted user to execute a command as the superuser or another user, as specified by the security policy.
15. How do you list all users in Linux?
    * Use the `cat /etc/passwd` command.

## File and Directory Permissions:

16. What are the three types of permissions in Linux?
    * The three types of permissions are read (`r`), write (`w`), and execute (`x`).
17. How do you change file permissions in Linux?
    * Use the `chmod` command followed by the desired permission mode and the filename.
18. What is the numerical representation of permissions in Linux?
    * The numerical representation of permissions uses a three-digit octal number, with each digit representing the permissions for the owner, group, and others, respectively.
19. How do you change the owner of a file in Linux?
    * Use the `chown` command followed by the new owner's username and the filename.
20. What is the purpose of the `chgrp` command?
    * The `chgrp` command changes the group ownership of a file or directory.

## Process Management:

21. How do you view running processes in Linux?
    * Use the `ps` command.
22. How do you kill a process in Linux?
    * Use the `kill` command followed by the process ID (PID).
23. What is a daemon in Linux?
    * A daemon is a background process that runs without user intervention.
24. How do you start a service in Linux?
    * Use the `systemctl start` command followed by the service name.
25. How do you stop a service in Linux?
    * Use the `systemctl stop` command followed by the service name.

## Package Management:

26. What is a package manager in Linux?
    * A package manager is a tool used to install, update, and manage software packages on a Linux system.
27. What is the package manager used in Debian-based distributions?
    * The package manager used in Debian-based distributions is `apt` (Advanced Package Tool).
28. What is the package manager used in Red Hat-based distributions?
    * The package manager used in Red Hat-based distributions is `yum` (Yellowdog Updater, Modified) or `dnf` (Dandified YUM).
29. How do you install a package in Linux?
    * Use the appropriate package manager with the `install` option followed by the package name.
30. How do you remove a package in Linux?
    * Use the appropriate package manager with the `remove` option followed by the package name.

## Networking:

31. How do you check the IP address of a Linux system?
    * Use the `ifconfig` or `ip addr` command.
32. How do you configure network settings in Linux?
    * Edit the network configuration files in the `/etc/network` directory or use tools like `ifconfig` or `ip`.
33. How do you restart the network service in Linux?
    * Use the `systemctl restart networking` command.
34. What is the purpose of the `/etc/hosts` file?
    * The `/etc/hosts` file maps hostnames to IP addresses and is used for hostname resolution.
35. What is DNS and how does it work?
    * DNS (Domain Name System) translates domain names into IP addresses, allowing users to access websites using human-readable names.

## System Monitoring and Performance:

36. How do you check system resource usage in Linux?
    * Use the `top` or `htop` command.
37. What is load average in Linux?
    * Load average represents the average number of processes waiting to run in the system's run queue over different time intervals.
38. How do you check disk usage in Linux?
    * Use the `df` command.
39. How do you check memory usage in Linux?
    * Use the `free` command.
40. What is the purpose of the `vmstat` command?
    * The `vmstat` command reports virtual memory statistics.

## System Logging:

41. What is syslog in Linux?
    * Syslog is a standard logging facility in Unix-like systems used to collect and manage log messages.
42. Where are syslog messages stored in Linux?
    * Syslog messages are stored in various files under the `/var/log` directory.
43. How do you view syslog messages in Linux?
    * Use the `tail` or `less` command to view syslog files such as `/var/log/syslog`.
44. What is the purpose of logrotate in Linux?
    * Logrotate is a utility used to manage log files by compressing, rotating, and deleting old log files to conserve disk space.
45. How do you configure logrotate in Linux?
    * Edit the configuration file `/etc/logrotate.conf` or create custom configuration files in the `/etc/logrotate.d` directory.

## System Security:

46. What is a firewall in Linux?
    * A firewall is a network security system that controls incoming and outgoing network traffic based on predetermined security rules.
47. What is the purpose of the `iptables` command?
    * The `iptables` command is used to configure firewall rules in Linux.
48. How do you check firewall rules in Linux?
    * Use the `iptables -L` command.
49. What is SELinux in Linux?
    * SELinux (Security-Enhanced Linux) is a Linux kernel security module that provides access control security policies.
50. How do you check SELinux status in Linux?
    * Use the `sestatus` command.

## System Backup and Recovery:

51. What is a backup in Linux?
    * A backup is a copy of data stored on a separate storage medium to protect against data loss.
52. How do you perform a backup in Linux?
    * Use backup utilities like `tar`, `rsync`, or dedicated backup software.
53. What is the purpose of cron in Linux?
    * Cron is a time-based job scheduler that allows users to schedule tasks to run periodically.
54. How do you schedule automated backups using cron?
    * Edit the crontab file using the `crontab -e` command and specify the backup command and schedule.
55. What is the purpose of RAID in Linux?
    * RAID (Redundant Array of Independent Disks) is a data storage technology that combines multiple disk drives into a logical unit for performance improvement and data redundancy.
56. What are the different RAID levels supported in Linux?
    * RAID 0, RAID 1, RAID 5, RAID 6, RAID 10, etc.
57. How do you recover data from a backup in Linux?
    * Use backup restoration tools or commands to restore data from backup files.
58. What is the purpose of the `tar` command in Linux?
    * The `tar` command is used to create, extract, and manipulate tar archives.
59. How do you create a compressed archive using tar in Linux?
    * Use the `-z` option with `tar` to create a compressed archive.
60. What is the purpose of the `dd` command in Linux?
    * The `dd` command is used to copy and convert files and data blocks.

## Kernel Management:

61. What is the Linux kernel?
    * The Linux kernel is the core component of the Linux operating system responsible for managing hardware resources and providing essential services to higher-level software.
62. How do you check the Linux kernel version?
    * Use the `uname -r` command.
63. What is a kernel module in Linux?
    * A kernel module is a piece of code that can be dynamically loaded and unloaded into the Linux kernel to extend its functionality.
64. How do you load a kernel module in Linux?
    * Use the `insmod` command followed by the module name.
65. How do you unload a kernel module in Linux?
    * Use the `rmmod` command followed by the module name.

## Virtualization:

66. What is virtualization in Linux?
    * Virtualization is the process of creating virtual instances of computing resources, such as virtual machines (VMs), on a physical computer.
67. What is a hypervisor in Linux?
    * A hypervisor is a software layer that allows multiple operating systems to run concurrently on a single physical computer.
68. What is KVM (Kernel-based Virtual Machine)?
    * KVM is a virtualization technology built into the Linux kernel that allows the Linux kernel to act as a hypervisor.
69. How do you create a virtual machine using KVM?
    * Use tools like `virt-install` or graphical management tools like Virt-Manager.
70. What is a container in Linux?
    * A container is a lightweight, isolated environment that shares the host system's kernel but has its own filesystem, process space, and network interfaces.
71. What is Docker?
    * Docker is a platform for developing, shipping, and running applications in containers.

## Shell Scripting:

72. What is a shell script in Linux?
    * A shell script is a text file containing a series of commands executed by the shell interpreter.
73. How do you create a shell script in Linux?
    * Create a text file with the desired commands and save it with a `.sh` extension.
74. What is the shebang line in a shell script?
    * The shebang line (`#!/bin/bash`) specifies the shell interpreter to use for executing the script.
75. How do you run a shell script in Linux?
    * Make the script executable using the `chmod +x` command and then run it using `./script.sh`.

## Text Processing:

76. What is grep in Linux?
    * Grep is a command-line utility used to search text files for patterns or regular expressions.
77. How do you search for a pattern in a file using grep?
    * Use the `grep` command followed by the pattern and filename.
78. What is sed in Linux?
    * Sed (stream editor) is a command-line utility used for text manipulation and processing.
79. How do you substitute text using sed?
    * Use the `s` command followed by the search pattern, replacement text, and filename.
80. What is awk in Linux?
    * Awk is a versatile programming language used for text processing and data extraction.

## System Administration Tasks:

81. How do you check system uptime in Linux?
    * Use the `uptime` command.
82. How do you shut down or restart a Linux system?
    * Use the `shutdown` command with the appropriate options (`-h` for shutdown, `-r` for restart).
83. How do you check disk space usage in Linux?
    * Use the `df` command.
84. How do you check system memory usage in Linux?
    * Use the `free` command.
85. What is the purpose of the `date` command in Linux?
    * The `date` command is used to display or set the system date and time.

## Backup and Recovery:

86. What is the purpose of a backup in Linux?
    * The purpose of a backup is to create copies of data to prevent data loss in the event of hardware failure, data corruption, or accidental deletion.
87. What is the difference between a full backup and an incremental backup?
    * A full backup copies all selected files and data, while an incremental backup only copies files that have changed since the last backup.
88. How do you perform a backup using rsync in Linux?
    * Use the `rsync` command followed by the source and destination directories.
89. How do you schedule automated backups using cron in Linux?
    * Edit the crontab file using the `crontab -e` command and specify the backup command and schedule.
90. How do you restore data from a backup in Linux?
    * Use backup restoration tools or commands to restore data from backup files.

## Networking:

91. How do you check network connectivity in Linux?
    * Use the `ping` command to test connectivity to a remote host.
92. How do you configure network settings in Linux?
    * Edit the network configuration files in the `/etc/network` directory or use tools like `ifconfig` or `ip`.
93. What is the purpose of the `/etc/hosts` file?
    * The `/etc/hosts` file maps hostnames to IP addresses and is used for hostname resolution.
94. How do you configure DNS settings in Linux?
    * Edit the `/etc/resolv.conf` file or use tools like `nmcli` or `systemd-resolve`.
95. How do you troubleshoot network issues in Linux?
    * Use tools like `ping`, `traceroute`, `netstat`, and `tcpdump` to diagnose network problems.

## Security:

96. What is a firewall in Linux?
    * A firewall is a network security system that controls incoming and outgoing network traffic based on predetermined security rules.
97. How do you configure firewall rules in Linux?
    * Use the `iptables` or `firewalld` command to configure firewall rules.
98. What is SELinux in Linux?
    * SELinux (Security-Enhanced Linux) is a Linux kernel security module that provides access control security policies.
99. How do you check SELinux status in Linux?
    * Use the `sestatus` command.
100. How do you secure a Linux system? - Secure a Linux system by keeping software up to date, configuring firewalls, using strong passwords, implementing SELinux policies, and regularly monitoring system logs.
