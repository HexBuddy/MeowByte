# API Security Fundamentals

## Exploring API Security

APIs (Application Programming Interfaces) are vital for modern applications, enabling seamless communication between different software systems. However, their widespread use also exposes them to significant security risks. Effective API security is essential to protect sensitive data and maintain system integrity.

{% embed url="https://www.youtube.com/watch?v=6WZ6S-qmtqY" %}

## OWASP Top 10 Background

The OWASP API Security Top 10 is a guide that helps developers and security teams tackle risks specific to APIs. It was created in 2019 because APIs were becoming more popular, needing their own set of security guidelines. While it shares similarities with the classic OWASP Top 10 for web apps, the API version focuses on unique API-related risks. Updated in 2024, it reflects current threats and best practices for securing APIs, making it crucial for anyone handling API security.

Here's a summarized version of the OWASP API Security Top 10 vulnerabilities presented in a table format for clarity:

| OWASP API Top 10                                   | Description                                                                    | Example                                                          | Prevention                                                                                           |
| -------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| 1. Broken Object Level Authorization               | Attackers manipulate IDs to access unauthorized data.                          | Attacker accesses User B's data by tampering with API requests.  | Implement strict access controls in application logic. Conduct regular automated testing.            |
| 2. Broken Authentication                           | Weak or absent authentication mechanisms.                                      | Weak passwords, lack of CAPTCHA, authentication in URLs.         | Implement robust authentication tailored to security requirements. Continuously test systems.        |
| 3. Broken Object Property Level Authorization      | Insecure modification of object properties.                                    | Changing account type through object ID manipulation.            | Ensure APIs return only necessary data. Validate inputs strictly to prevent unauthorized changes.    |
| 4. Unrestricted Resource Consumption               | Lack of controls on request volumes and frequencies.                           | Excessive queries overwhelming server resources.                 | Implement rate limiting, timeouts, and memory controls. Use application logic for additional checks. |
| 5. Broken Function Level Authorization             | Unauthorized access to sensitive API functions.                                | Using PUT or DELETE instead of GET to manipulate data.           | Secure functions with strict access controls. Thoroughly validate endpoint permissions.              |
| 6. Unrestricted Access to Sensitive Business Flows | Abuse of legitimate business processes for malicious purposes.                 | Automated purchase of entire inventory to disrupt market.        | Identify critical business flows prone to abuse. Implement controls to detect and prevent fraud.     |
| 7. Server Side Request Forgery                     | APIs accepting URLs as inputs vulnerable to internal or malicious site access. | Redirecting API requests to malicious URLs.                      | Validate and sanitize all user inputs, especially URLs. Implement strict input filtering.            |
| 8. Security Misconfiguration                       | Poorly configured server, network, or application settings.                    | Unpatched systems, unnecessary features enabled.                 | Implement robust security configurations. Regularly update and patch systems.                        |
| 9. Improper Inventory Management                   | Lack of visibility and control over API versions and endpoints.                | Exploiting vulnerabilities in outdated API versions.             | Maintain up-to-date API inventory. Implement policies for versioning and retirement.                 |
| 10. Unsafe Consumption of APIs                     | Vulnerabilities from using insecure third-party APIs.                          | Injecting malicious data or being redirected to malicious sites. | Validate and sanitize data from third-party APIs. Assess and enforce strict API security measures.   |





***
