---
description: >-
  For Bug Bounty Hunters, Penetration Testers, Private Investigators and OSINT
  Aggressors
---

# Enumeration And Information Gathering

## **Active Infrastructure Identification** <a href="#active-infrastructure-identification" id="active-infrastructure-identification"></a>

| Resource/Command                                                        | Description                                                |
| ----------------------------------------------------------------------- | ---------------------------------------------------------- |
| curl -I "http://${TARGET}"                                              | Display HTTP headers of the target webserver.              |
| whatweb -a https://www.facebook.com -v                                  | Technology identification.                                 |
| Wappalyzer                                                              | https://www.wappalyzer.com/                                |
| wafw00f -v https://$TARGET                                              | WAF Fingerprinting.                                        |
| Aquatone                                                                | https://github.com/michenriksen/aquatone                   |
| cat subdomain.list \| aquatone -out ./aquatone -screenshot-timeout 1000 | Makes screenshots of all subdomains in the subdomain.list. |

