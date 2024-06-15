# Information Gathering

## Passive Information Gathering

### Whois Enumeration

Perform Whois Lookup

* **Command-Line**: Use the `whois` command to query domain information.

### Google Hacking

### Netcraft

### Open-Source Code

### Shodan

### Security Headers and SSL/TLS

## Active Information Gathering

## **DNS Enumeration** <a href="#dns-enumeration" id="dns-enumeration"></a>

| Command                           | Description                                        |
| --------------------------------- | -------------------------------------------------- |
| nslookup $TARGET                  | Identify the A record for the target domain.       |
| nslookup -query=A $TARGET         | Identify the A record for the target domain.       |
| dig $TARGET @\<nameserver/IP>     | Identify the A record for the target domain.       |
| dig a $TARGET @\<nameserver/IP>   | Identify the A record for the target domain.       |
| nslookup -query=PTR               | Identify the PTR record for the target IP address. |
| dig -x @\<nameserver/IP>          | Identify the PTR record for the target IP address. |
| nslookup -query=ANY $TARGET       | Identify ANY records for the target domain.        |
| dig any $TARGET @\<nameserver/IP> | Identify ANY records for the target domain.        |
| nslookup -query=TXT $TARGET       | Identify the TXT records for the target domain.    |
| dig txt $TARGET @\<nameserver/IP> | Identify the TXT records for the target domain.    |
| nslookup -query=MX $TARGET        | Identify the MX records for the target domain.     |
| dig mx $TARGET @\<nameserver/IP>  | Identify the MX records for the target domain.     |

### TCP/UDP Port Scanning Theory

### Port Scanning with Nmap

### SMB Enumeration

### SMTP Enumeration

### SNMP Enumeration

