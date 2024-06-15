# Active Reconnaissance

## **Nmap**

*   **General Detection Scan**:

    ```bash
    $ nmap -sC -sV [target IP or domain]
    ```

    * **Purpose**: Identify services and versions using default scripts and service enumeration.
    * **Output**: List of open ports, detected services, and their versions.
*   **All Ports Scan**:

    ```bash
    $ nmap -p- [target IP or domain]
    ```

    * **Purpose**: Scan all 65,535 TCP ports to find services on non-standard ports.
    * **Output**: Comprehensive list of all open ports, helpful for discovering hidden APIs.

## **HTTP Enumeration**

Once HTTP services are identified, enumerate HTTP endpoints to discover potential API paths.

*   **Nmap HTTP Enumeration Script**:

    ```bash
    $ nmap --script=http-enum [target IP or domain]
    ```

    * **Purpose**: Identify web directories that may include API endpoints.
    * **Output**: List of discovered directories and their HTTP response codes.

## **OWASP Amass for Subdomain Enumeration**

OWASP Amass is invaluable for discovering subdomains and related assets, both actively and passively.

*   **Passive Mode**:

    ```bash
    $ amass enum -passive -d [target domain]
    ```

    * **Purpose**: Gather subdomains from various OSINT sources without direct interaction.
    * **Output**: List of discovered subdomains associated with the target.
*   **Active Mode**:

    ```bash
    $ amass enum -active -d [target domain]
    ```

    * **Purpose**: Perform DNS resolution, SSL certificate gathering, and more comprehensive subdomain discovery.
    * **Output**: Detailed list of active subdomains and related assets.

## **Gobuster for Directory Brute-Forcing**

Use Gobuster to brute-force directories and uncover hidden API paths that may not be linked from main pages.

*   **Basic Usage**:

    ```bash
    $ gobuster dir -u http://[target IP or domain] -w /path/to/wordlist.txt
    ```

    * **Purpose**: Discover hidden directories or API paths.
    * **Output**: List of discovered directories and their HTTP status codes.
* **Advanced Options**: Use `-x` to specify additional status codes to include, `-t` to set the number of concurrent threads for faster scanning, and `-o` to save results to a file.

## **Kiterunner for API Endpoint Discovery**

Kiterunner excels in discovering API endpoints by mimicking common API paths and methods.

*   **Basic Scan**:

    ```bash
    $ kr scan HTTP://[target IP or domain] -w ~/api/wordlists/data/kiterunner/routes-large.kite
    $ kr scan https://domain.com/api/ -w routes-large.kite -x 20
    $ kr scan https://domain.com/api/ -A=apiroutes-220828 -x 20
    $ kr brute https://domain.com/api/ -A=raft-large-words -x 20 -d=0
    $ kr brute https://domain.com/api/ -w /tmp/lang-english.txt -x 20 -d=0
    ```

    * **Purpose**: Discover specific API endpoints and their functionalities.
    * **Output**: List of discovered API endpoints and their responses.
*   **Brute-Force Option**:

    ```bash
    $ kr brute [target IP or domain] -w ~/path/to/wordlist.txt
    ```

    * **Purpose**: Brute-force API paths using a wordlist to find hidden or undocumented endpoints.
    * **Output**: Detailed list of potentially vulnerable or exposed API paths.

## **Burp Suite for Detailed API Testing**

Burp Suite is essential for detailed API testing, including interception, modification, and security analysis.

* **Interception Proxy**: Intercept and modify API requests/responses using Burp’s Proxy module.
  * **Purpose**: Analyze API traffic for vulnerabilities such as SQL injection, XSS, or authentication issues.
  * **Output**: Detailed request/response inspection, potential security findings.
* **Intruder Module**: Use Intruder to automate API request fuzzing and parameter manipulation for vulnerability detection.
  * **Purpose**: Identify injection points and test API endpoints systematically for security flaws.
  * **Output**: Vulnerable endpoints, potential exploit scenarios.

## **DevTools**

DevTools contains some highly underrated web application hacking tools. The following steps will help you easily and systematically filter through thousands of lines of code in order to find sensitive information in page sources. Begin by opening your target page, and then open DevTools with F12 or ctr-shift-I. Adjust the DevTools window until you have enough space to work with. Select the Network tab and then refresh the page (CTRL+r).

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/KAIntko1RBud1q6MVwBQ\_ActiveDiscovery5.PNG)

You can use the filter tool to search for any term you would like, such as "API", "v1", or "graphql". This is a quick way to find API endpoints in use. You can also leave the Devtools Network tab open while you perform actions on the web page. For example, let's check out what happens if we leave the DevTools open while we authenticate to crAPI. You should see a new request pop up. At this point, you can dive deeper into the request by right-clicking on one of the requests and selecting "Edit and Resend".

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/JHIANpvkSDONA1eM3T0S\_ActiveDiscovery7.PNG)

This will allow you to check out the request in the browser, edit the headers/request body, and send it back to the API provider. Although this is a great DevTools feature, you may want to move into a browser that was meant for interacting with APIs. You can use DevTools to migrate individual requests over to Postman using cURL.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/dKkYPAvmRTM4i4y825GQ\_ActiveDiscovery7-5.PNG)

Once you have copied the desired request, open Postman. Select Import and click on the "Raw text" tab. Paste in the cURL request and select import.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/NPybx1iQaeK63RN9bsTz\_ActiveDiscovery8.PNG)

&#x20;Once the request has been imported it will have all of the necessary headers and the request body necessary to make additional requests in Postman. This is a great way to quickly interact with an API and interact with a single API request. To automatically build out a more complete Postman Collection check out the next module which is on Reverse Engineering an API.

Reconnaissance is extremely important when testing APIs. Discovering API endpoints is a necessary first step when attacking APIs. Good recon also has the added benefit of potentially providing you with the keys to the castle in the form of API keys, passwords, tokens, and other useful information disclosures.

## **Additional Techniques**

* **Postman Integration**:
  * Import cURL requests from DevTools to Postman for API testing.
  * Automate request chaining and scenario-based testing.
* **Scripting with Python Requests**:
  * Write Python scripts using `requests` library to automate API interactions.
  * Test for authentication bypass, parameter manipulation, and more.

***
