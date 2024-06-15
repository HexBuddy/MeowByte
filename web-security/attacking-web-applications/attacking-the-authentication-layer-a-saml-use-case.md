# Attacking the Authentication Layer – a SAML Use Case

{% hint style="info" %}
**Welcome to the third chapter, where we analyze our vulnerable applications with a Capture the Flag (CTF) exercise on Security Assertion Markup Language (SAML).**
{% endhint %}

## What is SAML?

SAML is an **XML-based standard** for managing _**federated authentication and authorization**_, focusing on web SSO. It is the dominant technology for enterprise-level SSO.&#x20;

It was developed by the **Security Services Technical Committee (SSTC)** of the **Organization for the Advancement of Structured Information Standards (OASIS)** and is currently at version 2.0.

## Web Browser SSO Profile

SAML supports various profiles tailored for different implementation scenarios. The most relevant for web applications is the **Web Browser SSO Profile**. This profile facilitates user authentication via a workflow involving a Service Provider (SP) and an Identity Provider (IdP).

### SAML Workflow

Here’s a simplified overview of the SAML workflow for the Web Browser SSO Profile:

1. **Resource Access Request**: The user initiates a request to access a resource on a web application (SP).
2. **SAML Request Generation**: If the user is not authenticated, the SP generates a SAML request. This request includes details like the Assertion Consumer Service (ACS) URL, IdP address, request ID, timestamp, protocol type, and issuer.
3. **SAML Request Transmission**: The SAML request is encoded in base64 and transmitted via the user's browser to the IdP.
4. **SAML Request Verification & Authentication**: The IdP verifies the request and presents an authentication screen to the user, typically asking for credentials.
5. **SAML Response Generation**: Upon successful authentication, the IdP creates a SAML response containing the user’s information, such as identity attributes and cryptographic signatures to ensure data integrity.
6. **SAML Response Transmission**: The SAML response, encoded similarly to the request, is sent to the SP's ACS URL through an HTTP POST request via the user's browser.
7. **SAML Response Verification**: The SP parses and verifies the SAML response.
8. **Resource Access Grant**: If the response is valid, the SP grants the user access to the requested resource.

## Vulnerabilities in SAML

SAML implementations can be vulnerable to several issues, particularly during the transmission and verification of SAML requests and responses. Key areas of vulnerability include:

* **Software Issues**:
  * Implementations that do not adhere strictly to the SAML standard.
  * Software with known vulnerabilities.
* **Configuration Problems**: Secure software that is nonetheless misconfigured, leading to potential security weaknesses.
* **XML-Based Attacks**: Exploiting vulnerabilities related to XML parsing and open redirects.
* **General Security Flaws**: Issues related to input validation, authorization, and session management.

Exploiting SAML vulnerabilities often involves tampering with SAML requests or responses during transmission, leveraging the browser's role as an intermediary. Cryptographic signatures are crucial for protecting the integrity of these messages.

## Alternative Authentication Methods

While SAML is widely used for federated authentication, several other methods are also common in HTTP contexts:

* **HTTP Authentication**:
  * **Basic Authentication**: Sends username and password encoded in base64.
  * **Digest Authentication**: Uses hashing instead of base64 encoding.
* **HTTPS Authentication**:
  * **Certificate-Based Authentication**: Utilizes SSL/TLS certificates to authenticate both server and client.
* **Application-Level Authentication**:
  * **Form/Cookie/Token-Based**: Traditional method using cookies to store authentication tokens.
  * **OAuth**: Allows resource sharing between applications without exchanging credentials.
  * **OpenID**: Delegates authentication to an external authorization server.
  * **JSON Web Token (JWT)**: An open standard for creating authentication tokens.

## How to discover and exploit vulnerabilities in SAML

Let’s start by installing SAML Raider and see whether everything works with the happy case.

Installing SAML Raider Follow these steps to install SAML Raider:&#x20;

1. Run BurpSuite
2. From the Burp interface, click on Extensions and then on BApp Store.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p><strong>BApp Store In BurpSuite</strong></p></figcaption></figure>

3. Search For "SAML Raider" On the Search Bar on the Left At the Top

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

4. Click on the Result Found

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

5. Scroll All the way down and install it

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

In my Case I have installed before so it appears for me Reinstall

The first thing we do is to evaluate the base case, or happy case, in which everything works. Run the lab from the GitHub repository.

### Start the scenario

1. Download the GitHub repository locally

```
git clone https://github.com/HexBuddy/Attacking-and-Exploiting-Modern-Web-Applications
```

1. Go in the `Chapter03` directory

```
cd Chapter03
```

3. Run `docker compose up`:

```
docker compose up
```

### Configure the appliacion for each paragraph

To configure the application use a different browser than the one you are using to do the tests and:

1. Connect to the address of the service provider `http://localhost:8000/`
2. Login with the user `yavanna` and password `G0od-LuckGu3ssingThisButHeyItCouldHappenRight?`
3. Click the `SAML Settings` item on the menu.

Then you can go ahead and configure the application as shown below for the various paragraphs of the scenario.

### Verifying whether it is possible to send information without signature

Check only `validAssertion` and `validMessage`.

### Verifying whether it is possible to use a self-signed certificate

Check only `wantMessagesSigned` and `wantAssertionsSigned`.

### Verifying whether it is possible to use XML Signature Wrapping (XSW)

Uncheck all.

***

### **Let’s start by looking at a normal authentication flow with SAML:**

