# Intrusion Detection and Prevention

### Table of Contents

1. [Cheat Sheet](intrusion-detection-and-prevention.md#cheat-sheet)
2. [Deploying Fail2ban for Intrusion Prevention](intrusion-detection-and-prevention.md#deploying-fail2ban-for-intrusion-prevention)
3. [Setting Up OSSEC for Log Monitoring and File Integrity Checking](intrusion-detection-and-prevention.md#setting-up-ossec-for-log-monitoring-and-file-integrity-checking)
4. [Deploying Snort for Network Intrusion Detection](intrusion-detection-and-prevention.md#deploying-snort-for-network-intrusion-detection)
5. [Using Tripwire for File Integrity Monitoring](intrusion-detection-and-prevention.md#using-tripwire-for-file-integrity-monitoring)
6. [Setting Up a HIPS with AIDE](intrusion-detection-and-prevention.md#setting-up-a-hips-with-aide)
7. [Endpoint Detection and Response (EDR) on Linux](intrusion-detection-and-prevention.md#endpoint-detection-and-response-edr-on-linux)

***

## Cheat Sheet

| **Task**                              | **Command (Debian/Ubuntu)**                                                                 | **Command (Arch Linux)**         | **Command (CentOS/Red Hat)**                               |
| ------------------------------------- | ------------------------------------------------------------------------------------------- | -------------------------------- | ---------------------------------------------------------- |
| Install Fail2ban                      | `sudo apt install fail2ban`                                                                 | `sudo pacman -S fail2ban`        | `sudo yum install fail2ban` or `sudo dnf install fail2ban` |
| Start Fail2ban Service                | `sudo systemctl start fail2ban`                                                             | `sudo systemctl start fail2ban`  | `sudo systemctl start fail2ban`                            |
| Check Fail2ban Status                 | `sudo systemctl status fail2ban`                                                            | `sudo systemctl status fail2ban` | `sudo systemctl status fail2ban`                           |
| Install OSSEC                         | `wget https://bintray.com/ossec/ossec-hids/download_file?file_path=ossec-hids-3.6.0.tar.gz` | `yaourt -S ossec-hids`           | `sudo yum install ossec-hids`                              |
| Start OSSEC Service                   | `sudo /var/ossec/bin/ossec-control start`                                                   | `sudo systemctl start ossec`     | `sudo systemctl start ossec-hids`                          |
| Check OSSEC Status                    | `sudo /var/ossec/bin/ossec-control status`                                                  | `sudo systemctl status ossec`    | `sudo systemctl status ossec-hids`                         |
| Install Snort                         | `sudo apt install snort`                                                                    | `sudo pacman -S snort`           | `sudo yum install snort` or `sudo dnf install snort`       |
| Start Snort                           | `sudo systemctl start snort`                                                                | `sudo systemctl start snort`     | `sudo systemctl start snort`                               |
| Check Snort Status                    | `sudo systemctl status snort`                                                               | `sudo systemctl status snort`    | `sudo systemctl status snort`                              |
| Install Tripwire                      | `sudo apt install tripwire`                                                                 | `sudo pacman -S tripwire`        | `sudo yum install tripwire` or `sudo dnf install tripwire` |
| Initialize Tripwire Database          | `sudo tripwire --init`                                                                      | `sudo tripwire --init`           | `sudo tripwire --init`                                     |
| Run Tripwire Check                    | `sudo tripwire --check`                                                                     | `sudo tripwire --check`          | `sudo tripwire --check`                                    |
| Install AIDE                          | `sudo apt install aide`                                                                     | `sudo pacman -S aide`            | `sudo yum install aide` or `sudo dnf install aide`         |
| Initialize AIDE Database              | `sudo aideinit`                                                                             | `sudo aide --init`               | `sudo aide --init`                                         |
| Run AIDE Check                        | `sudo aide --check`                                                                         | `sudo aide --check`              | `sudo aide --check`                                        |
| EDR Installation (Varies by Software) | Varies by EDR solution                                                                      | Varies by EDR solution           | Varies by EDR solution                                     |
| EDR Configuration and Monitoring      | Varies by EDR solution                                                                      | Varies by EDR solution           | Varies by EDR solution                                     |

***

## Deploying Fail2ban for Intrusion Prevention

Fail2ban is a popular intrusion prevention framework that protects servers from brute-force attacks. It works by monitoring log files and banning IPs that show malicious signs, such as too many password failures.

**Installing Fail2ban**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install fail2ban
    ```

    Explanation: This command installs Fail2ban from the default package repositories.
*   **Arch Linux**:

    ```sh
    sudo pacman -S fail2ban
    ```

    Explanation: This command installs Fail2ban using the Pacman package manager.
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install fail2ban
    ```

    or

    ```sh
    sudo dnf install fail2ban
    ```

    Explanation: These commands install Fail2ban using the Yum or DNF package managers, depending on your system's configuration.

**Configuring Fail2ban**

1.  **Create Local Configuration File**:

    ```sh
    sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
    ```

    Explanation: Copying the default configuration file to `jail.local` allows you to make custom changes without affecting the default settings.
2.  **Edit Configuration**:

    ```sh
    sudo nano /etc/fail2ban/jail.local
    ```

    Example configuration:

    ```ini
    [DEFAULT]
    bantime  = 1h
    findtime  = 10m
    maxretry = 5

    [sshd]
    enabled = true
    ```

    Explanation: This configuration sets default ban time, find time, and maximum retry attempts. It also enables protection for the SSH service.

**Starting and Monitoring Fail2ban**

*   **Start Fail2ban**:

    ```sh
    sudo systemctl start fail2ban
    ```

    Explanation: This command starts the Fail2ban service, activating the protections configured.
*   **Enable Fail2ban at Boot**:

    ```sh
    sudo systemctl enable fail2ban
    ```

    Explanation: This command ensures Fail2ban starts automatically at boot.
*   **Check Fail2ban Status**:

    ```sh
    sudo systemctl status fail2ban
    ```

    Explanation: This command checks the current status of the Fail2ban service, confirming it is active and running correctly.
*   **Monitor Logs**:

    ```sh
    sudo fail2ban-client status
    sudo fail2ban-client status sshd
    ```

    Explanation: These commands provide overall status and detailed status for the SSH jail, showing banned IP addresses and other relevant information.

***

## Setting Up OSSEC for Log Monitoring and File Integrity Checking

OSSEC is a comprehensive open-source Host Intrusion Detection System (HIDS) for log analysis, integrity checking, Windows registry monitoring, rootkit detection, time-based alerting, and active response.

**Installing OSSEC**

*   **Download OSSEC**:

    ```sh
    wget https://bintray.com/ossec/ossec-hids/download_file?file_path=ossec-hids-3.6.0.tar.gz
    ```

    Explanation: This command downloads the OSSEC installation package.
*   **Extract and Install**:

    ```sh
    tar -xvzf ossec-hids-3.6.0.tar.gz
    cd ossec-hids-3.6.0
    sudo ./install.sh
    ```

    Explanation: These commands extract the downloaded package and run the installation script.

**Configuring OSSEC**

1.  **Edit Configuration File**:

    ```sh
    sudo nano /var/ossec/etc/ossec.conf
    ```

    Example configuration:

    ```xml
    <ossec_config>
      <global>
        <email_notification>yes</email_notification>
        <email_to>admin@example.com</email_to>
        <smtp_server>smtp.example.com</smtp_server>
        <email_from>ossec@example.com</email_from>
        <white_list>127.0.0.1</white_list>
      </global>

      <syscheck>
        <frequency>3600</frequency>
        <directories check_all="yes">/etc,/usr/bin,/usr/sbin</directories>
      </syscheck>

      <localfile>
        <log_format>syslog</log_format>
        <location>/var/log/auth.log</location>
      </localfile>

      <rootcheck>
        <check_files>yes</check_files>
        <check_trojans>yes</check_trojans>
      </rootcheck>
    </ossec_config>
    ```

    Explanation: This configuration sets up global settings like email notifications, log settings, and whitelists. The `syscheck` section configures file integrity monitoring, specifying which directories to check and how frequently. The `localfile` section indicates which local log files to monitor, and the `rootcheck` section enables rootkit detection.
2.  **Start OSSEC**:

    ```sh
    sudo /var/ossec/bin/ossec-control start
    ```

    Explanation: Starting OSSEC activates the service, initiating log monitoring and file integrity checking based on the configured settings.

**Using OSSEC**

*   **Check OSSEC Status**:

    ```sh
    sudo /var/ossec/bin/ossec-control status
    ```

    Explanation: This command provides the status of the OSSEC service, including whether it is running and if all configured components are active.
*   **View OSSEC Logs**:

    ```sh
    sudo tail -f /var/ossec/logs/ossec.log
    ```

    Explanation: Viewing the OSSEC logs helps monitor real-time activity and alerts, useful for immediate response to potential intrusions.
*   **Check Alerts**:

    ```sh
    sudo tail -f /var/ossec/logs/alerts/alerts.log
    ```

    Explanation: The alerts log contains specific

alerts generated by OSSEC, providing detailed information on detected issues and incidents.

***

## Deploying Snort for Network Intrusion Detection

Snort is an open-source network intrusion detection system (NIDS) capable of performing real-time traffic analysis and packet logging. It can detect a variety of attacks and probes, such as buffer overflows, stealth port scans, and more.

**Installing Snort**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install snort
    ```

    Explanation: This command installs Snort from the default package repositories.
*   **Arch Linux**:

    ```sh
    sudo pacman -S snort
    ```

    Explanation: This command installs Snort using the Pacman package manager.
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install snort
    ```

    or

    ```sh
    sudo dnf install snort
    ```

    Explanation: These commands install Snort using the Yum or DNF package managers, depending on your system's configuration.

**Configuring Snort**

1.  **Edit Configuration File**:

    ```sh
    sudo nano /etc/snort/snort.conf
    ```

    Example configuration:

    ```ini
    var HOME_NET any
    var EXTERNAL_NET any

    include $RULE_PATH/local.rules
    include $RULE_PATH/bad-traffic.rules
    include $RULE_PATH/exploit.rules
    include $RULE_PATH/scan.rules
    include $RULE_PATH/finger.rules
    include $RULE_PATH/ftp.rules
    include $RULE_PATH/telnet.rules
    include $RULE_PATH/smtp.rules
    include $RULE_PATH/rpc.rules
    include $RULE_PATH/rservices.rules
    include $RULE_PATH/dos.rules
    include $RULE_PATH/ddos.rules
    include $RULE_PATH/dns.rules
    include $RULE_PATH/tftp.rules
    include $RULE_PATH/web-cgi.rules
    include $RULE_PATH/web-coldfusion.rules
    include $RULE_PATH/web-frontpage.rules
    include $RULE_PATH/web-iis.rules
    include $RULE_PATH/web-misc.rules
    include $RULE_PATH/web-client.rules
    include $RULE_PATH/web-php.rules
    include $RULE_PATH/imap.rules
    include $RULE_PATH/p2p.rules
    include $RULE_PATH/voip.rules
    include $RULE_PATH/icmp.rules
    include $RULE_PATH/icmp-info.rules
    include $RULE_PATH/virus.rules
    include $RULE_PATH/attack-responses.rules
    include $RULE_PATH/experimental.rules
    ```

    Explanation: This configuration sets network variables and includes various rule sets to define what types of traffic and attacks Snort should monitor and log.
2.  **Update Rules**:

    ```sh
    sudo snort -T -c /etc/snort/snort.conf
    ```

    Explanation: This command tests the Snort configuration to ensure there are no errors in the setup.

**Running Snort**

*   **Start Snort**:

    ```sh
    sudo systemctl start snort
    ```

    Explanation: This command starts the Snort service, activating network traffic monitoring based on the configured rules.
*   **Enable Snort at Boot**:

    ```sh
    sudo systemctl enable snort
    ```

    Explanation: This command ensures Snort starts automatically at boot, maintaining continuous network monitoring.
*   **Check Snort Status**:

    ```sh
    sudo systemctl status snort
    ```

    Explanation: This command checks the current status of the Snort service, confirming it is active and running correctly.
*   **Monitor Snort Logs**:

    ```sh
    sudo tail -f /var/log/snort/alert
    ```

    Explanation: Viewing Snort logs helps monitor real-time alerts and detected intrusions, useful for immediate response to potential threats.

***

## Using Tripwire for File Integrity Monitoring

Tripwire is a file integrity monitoring tool that helps detect unauthorized changes to files and directories, ensuring system integrity and security.

**Installing Tripwire**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install tripwire
    ```

    Explanation: This command installs Tripwire from the default package repositories.
*   **Arch Linux**:

    ```sh
    sudo pacman -S tripwire
    ```

    Explanation: This command installs Tripwire using the Pacman package manager.
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install tripwire
    ```

    or

    ```sh
    sudo dnf install tripwire
    ```

    Explanation: These commands install Tripwire using the Yum or DNF package managers, depending on your system's configuration.

**Configuring Tripwire**

1.  **Initialize Database**:

    ```sh
    sudo tripwire --init
    ```

    Explanation: This command initializes the Tripwire database, creating a baseline snapshot of the system files for integrity checks.
2.  **Edit Policy File**:

    ```sh
    sudo nano /etc/tripwire/twpol.txt
    ```

    Example configuration:

    ```ini
    # Tripwire configuration policy file
    /bin         -> $(ReadOnly) ;
    /sbin        -> $(ReadOnly) ;
    /usr/bin     -> $(ReadOnly) ;
    /usr/sbin    -> $(ReadOnly) ;
    /etc         -> $(Dynamic) ;
    /lib         -> $(Dynamic) ;
    /lib64       -> $(Dynamic) ;
    /var/log     -> $(Growing) ;
    ```

    Explanation: This configuration sets policies for different directories, specifying how Tripwire should monitor them (e.g., read-only, dynamic, growing).
3.  **Update Policy**:

    ```sh
    sudo tripwire --update-policy /etc/tripwire/twpol.txt
    ```

    Explanation: This command updates Tripwire's internal policies based on the modified policy file.

**Using Tripwire**

*   **Run Integrity Check**:

    ```sh
    sudo tripwire --check
    ```

    Explanation: This command performs an integrity check, comparing the current state of the system files to the baseline snapshot.
*   **View Tripwire Report**:

    ```sh
    sudo nano /var/lib/tripwire/report/<report-file>
    ```

    Explanation: Viewing the Tripwire report provides detailed information on any detected changes or potential issues.
*   **Update Database After Changes**:

    ```sh
    sudo tripwire --update --twrfile /var/lib/tripwire/report/<report-file>
    ```

    Explanation: After verifying that detected changes are legitimate, this command updates the Tripwire database to include those changes in the new baseline.

***

## Setting Up a HIPS with AIDE

AIDE (Advanced Intrusion Detection Environment) is a file and directory integrity checker that helps detect unauthorized changes to the system.

**Installing AIDE**

*   **Debian/Ubuntu**:

    ```sh
    sudo apt install aide
    ```

    Explanation: This command installs AIDE from the default package repositories.
*   **Arch Linux**:

    ```sh
    sudo pacman -S aide
    ```

    Explanation: This command installs AIDE using the Pacman package manager.
*   **CentOS/Red Hat**:

    ```sh
    sudo yum install aide
    ```

    or

    ```sh
    sudo dnf install aide
    ```

    Explanation: These commands install AIDE using the Yum or DNF package managers, depending on your system's configuration.

**Configuring AIDE**

1.  **Initialize Database**:

    ```sh
    sudo aideinit
    ```

    Explanation: This command initializes the AIDE database, creating a baseline snapshot of the system files for integrity checks.
2.  **Edit Configuration File**:

    ```sh
    sudo nano /etc/aide/aide.conf
    ```

    Example configuration:

    ```ini
    /bin    p+i+n+u+g+s+b+m+c+md5+sha1
    /sbin   p+i+n+u+g+s+b+m+c+md5+sha1
    /lib    p+i+n+u+g+s+b+m+c+md5+sha1
    /lib64  p+i+n+u+g+s+b+m+c+md5+sha1
    /usr/bin p+i+n+u+g+s+b+m+c+md5+sha1
    /usr/sbin p+i+n+u+g+s+b+m+c+md5+sha1
    /etc    p+i+n+u+g+s+b+m+c+md5+sha1
    ```

    Explanation: This configuration sets the rules for AIDE to monitor various directories, specifying the attributes to check, such as permissions, inode, owner, group, size, block count, mtime, ctime, MD5, and SHA1 hashes.
3.  **Update Configuration**:

    ```sh
    sudo aide --init
    sudo cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db
    ```

    Explanation: Initializing AIDE with the new configuration and copying the newly created database to replace the old one ensures the updated rules are applied.

**Using AIDE**

*   **Run Integrity Check**:

    ```sh
    sudo aide --check
    ```

    Explanation: This command performs an integrity check, comparing the current state of the system files to the baseline snapshot.
*   **View AIDE Report**:

    ```sh
    sudo nano /var/lib/aide/aide.log
    ```

    Explanation: Viewing the AIDE log provides detailed information on any detected changes or potential issues.
*   **Update Database After Changes**:

    ```sh
    sudo aide --update
    sudo cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db


    ```

    Explanation: After verifying that detected changes are legitimate, this command updates the AIDE database to include those changes in the new baseline.

***

## Endpoint Detection and Response (EDR) on Linux

Endpoint Detection and Response (EDR) solutions provide advanced monitoring, detection, and response capabilities for endpoint devices. EDR tools typically include real-time monitoring, advanced threat detection, and automated responses to security incidents.

**Choosing an EDR Solution**

Popular EDR solutions for Linux include:

* **CrowdStrike Falcon**
* **Carbon Black**
* **SentinelOne**
* **Sophos Intercept X**

**Installing EDR**

Installation steps vary by EDR solution. Generally, the process involves:

1.  **Download Installation Package**:

    ```sh
    wget <URL_to_EDR_installation_package>
    ```

    Explanation: This command downloads the EDR installation package from the vendor's website.
2.  **Run Installation Script**:

    ```sh
    sudo bash <installation_script.sh>
    ```

    Explanation: Running the installation script sets up the EDR agent on the endpoint.

**Configuring EDR**

Configuration steps vary by EDR solution. Typically, this involves:

1. **Register Endpoint**: Register the endpoint with the EDR management console, usually by providing a unique identifier or activation key.
2. **Set Policies**: Define security policies, such as monitoring rules, alert thresholds, and automated responses, through the EDR management console.

**Using EDR**

* **Monitor Endpoint Activity**: Use the EDR management console to monitor real-time activity and alerts from the endpoint.
* **Investigate Incidents**: Analyze detected incidents using the EDR's forensic tools to determine the root cause and take appropriate actions.
* **Respond to Threats**: Use automated or manual response options to mitigate detected threats, such as isolating the endpoint, blocking malicious processes, or removing malware.

***

This comprehensive guide provides detailed instructions and explanations for deploying various Host Intrusion Detection Systems (HIDS) and Endpoint Detection and Response (EDR) solutions on Linux, ensuring robust security for your systems.
