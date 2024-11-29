# BugBountyMastery

## 🚀 Introduction
This repository contains a comprehensive bug bounty methodology, designed for anyone interested in getting started or improving their skills in bug hunting. The methodology covers the entire process from reconnaissance to reporting vulnerabilities, with a focus on common tools, payloads, and techniques.

## 🧩 Table of Contents
1. [🔍 Reconnaissance](#1-reconnaissance)
2. [🛠️ Vulnerability Analysis](#2-vulnerability-analysis)
3. [💥 Exploitation](#3-exploitation)
4. [📝 Reporting](#4-reporting)
5. [💡 Common Payloads](#5-common-payloads)
6. [📚 Resources](#6-resources)

---

## 1. 🔍 Reconnaissance
**Purpose**: Gather information about the target to identify potential attack surfaces.

### Steps to Follow:
- Identify subdomains and live hosts.
- Analyze services and technologies in use (e.g., CMS, frameworks).
- Scan for open ports and services.
- **Identify DNS records**: DNS records may provide additional insights into the infrastructure.
- **Fingerprint the Web Server**: Find server software, version, and potential vulnerabilities.

### Tools:
- **Sublist3r**: A tool to find subdomains using various sources like Google and VirusTotal.
    ```bash
    sublist3r -d example.com -o subdomains.txt
    ```

- **HTTPX**: Validates if subdomains are active and responsive.
    ```bash
    cat subdomains.txt | httpx -o active_hosts.txt
    ```

- **Nmap**: Scans for open ports and identifies services.
    ```bash
    nmap -sC -sV -iL active_hosts.txt -oN nmap_scan.txt
    ```

- **Wappalyzer**: Identifies technologies in use on a website (e.g., PHP, WordPress, React).

- **Amass**: A comprehensive open-source tool for network mapping and subdomain enumeration.  
  [GitHub - Amass](https://github.com/OWASP/Amass)
    ```bash
    amass enum -d example.com -o amass_subdomains.txt
    ```

- **Shodan**: Provides a search engine for internet-connected devices, helping you identify vulnerable devices.  
  [Website - Shodan](https://www.shodan.io/)

- **Fierce**: A DNS reconnaissance tool for gathering information about subdomains and other DNS records.  
  [GitHub - Fierce](https://github.com/mschwager/fierce)
    ```bash
    fierce --domain example.com
    ```

- **DNSdumpster**: A free online tool for finding subdomains, DNS records, and other related information.  
  [Website - DNSdumpster](https://dnsdumpster.com/)

- **WhatWeb**: A tool that identifies the technologies used by websites. It can identify web servers, CMS, and JavaScript frameworks.  
  [GitHub - WhatWeb](https://github.com/urbanadventurer/WhatWeb)
    ```bash
    whatweb example.com
    ```

### Key Tips:
- Save all results from your reconnaissance as they will be needed in later stages.
- Be mindful of staying within the "scope" defined by the target.
- Collect IP addresses and geolocation data of servers for further analysis.

---

## 2. 🛠️ Vulnerability Analysis
**Purpose**: Identify weaknesses in the application's attack surfaces.

### Steps to Follow:
- Manually test for common vulnerabilities.
- Perform fuzzing to find hidden endpoints or parameters.
- Validate and confirm vulnerabilities.
- **Check for sensitive files and configurations**: Look for files like `robots.txt`, `.git`, `/.env`, or others that might disclose sensitive information.
- **Scan for weak SSL/TLS configurations**: SSL Labs' tool can help assess the target's SSL/TLS security.

### Tools:
- **Burp Suite Community Edition**: Intercepts and manipulates traffic between client and server.

- **Dirb**: Brute-forces directories and files on the server.
    ```bash
    dirb https://example.com /path/to/wordlist.txt -o directories.txt
    ```

- **SQLmap**: Automates the detection and exploitation of SQL injection vulnerabilities.
    ```bash
    sqlmap -u "https://example.com/page?parameter=value" --dbs
    ```

- **XSStrike**: Scans for XSS vulnerabilities and tests with various payloads.
    ```bash
    python3 xsstrike.py -u "https://example.com/search?q=test"
    ```

- **Gobuster**: A tool for directory and file busting, also supports DNS subdomain brute-forcing.  
  [GitHub - Gobuster](https://github.com/OJ/gobuster)
    ```bash
    gobuster dir -u https://example.com -w /path/to/wordlist.txt
    ```

- **Nikto**: A web server scanner that detects vulnerabilities like outdated software, security misconfigurations, and more.
    ```bash
    nikto -h https://example.com
    ```

- **FFUF (Fuzz Faster U Fool)**: A fast web fuzzer that can find hidden endpoints.  
  [GitHub - FFUF](https://github.com/ffuf/ffuf)
    ```bash
    ffuf -u https://example.com/FUZZ -w /path/to/wordlist.txt
    ```

- **Burp Suite Intruder**: The Intruder feature can be used to brute-force parameters or perform fuzzing on endpoints.

- **Metasploit**: An exploitation framework that includes numerous pre-built exploits. Use it to test known vulnerabilities.  
  [GitHub - Metasploit](https://github.com/rapid7/metasploit-framework)
    ```bash
    msfconsole
    ```

- **Retire.js**: A tool that scans for vulnerable JavaScript libraries that might be used on the website.  
  [GitHub - Retire.js](https://github.com/RetireJS/retire.js)
    ```bash
    retire --path /path/to/project
    ```

- **Wfuzz**: Another great fuzzing tool for testing web applications and APIs.  
  [GitHub - Wfuzz](https://github.com/xmendez/wfuzz)
    ```bash
    wfuzz -c -z file,/path/to/wordlist.txt -u "https://example.com/FUZZ"
    ```

- **TLS/SSL Testing**:
   - **SSL Labs**: Use SSL Labs to test SSL/TLS strength of the target website.  
     [SSL Labs](https://www.ssllabs.com/ssltest/)
   - **testssl.sh**: A command-line tool for testing SSL/TLS vulnerabilities.  
     [GitHub - testssl.sh](https://github.com/drwetter/testssl.sh)
    ```bash
    testssl.sh example.com
    ```

### Key Tips:
- Always test edge cases and uncommon input combinations.
- Review the target's documentation or public repositories for any potential security issues.
- Leverage the knowledge of popular vulnerabilities in open-source tools and frameworks.

---

## 3. 💥 Exploitation
**Purpose**: Demonstrate the vulnerability and show its impact.

### Examples of Vulnerabilities and Payloads:
- **XSS (Cross-Site Scripting)**: Paste a payload like `<script>alert('XSS')</script>` in a form field or URL.
- **SQL Injection**: Try manipulating input in forms or URL with the payload `' OR '1'='1' --`.
- **Command Injection**: Test if the application executes system commands via user input with the payload `; ls -la`.

### Example Payloads:
- **XSS**: 
    ```html
    <script>alert('XSS')</script>
    ```
    **Placement**: Form field, search bar, or URL parameter.  
    **Purpose**: Tests if JavaScript is executed.

- **SQL Injection**:
    ```sql
    ' OR '1'='1' --
    ```
    **Placement**: Login form, URL parameter, or any user input field.  
    **Purpose**: Tests if the application is vulnerable to SQL injection.

- **Command Injection**:
    ```bash
    ; ls -la
    ```
    **Placement**: URL parameter, form field.  
    **Purpose**: Tests if system commands can be executed via user input.

---

## 4. 📝 Reporting
**Purpose**: Document findings clearly to help the development team fix the issue.

### Report Structure:
- **Title**: [Type of vulnerability] in [target].
- **Summary**: A brief description of the issue.
- **Reproduction**: Step-by-step instructions to reproduce the bug.
- **Impact**: What could go wrong if the bug is exploited?
- **Suggested Fix**: How to resolve the bug?

### Tools for Documentation:
- **Obsidian** / **Notion**: Note-taking tools for keeping track of findings.
- **OBS Studio**: Record evidence of vulnerabilities to demonstrate the steps involved.

---

## 5. 💡 Common Payloads

| Vulnerability Type | Payload                                | Placement               | Purpose                                                   |
|--------------------|----------------------------------------|-------------------------|-----------------------------------------------------------|
| **XSS**            | `<script>alert('XSS')</script>`         | Search Field/Form       | Tests if JavaScript is executed.                          |
| **SQL Injection**  | `' OR '1'='1' --`                      | URL/Login Field         | Tests for unprotected SQL queries.                       |
| **Command Injection** | `; ls -la`                          | URL/Input Field         | Tests if system commands are executed.                    |
| **CSRF**           | `<img src="http://example.com/change?param=value">` | HTML                   | Tests if an unauthenticated change can be triggered.      |

---

## 6. 📚 Resources to keep yourself updated:

- [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings): A comprehensive list of useful payloads for various vulnerabilities.
- [Hacker101](https://www.hacker101.com/): Free security training resources by HackerOne.
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/): A series of best practice cheat sheets for various security topics.
- [Bugcrowd University](https://www.bugcrowd.com/bugcrowd-university/): Learn from Bugcrowd’s bug bounty platform and training courses.
- [PentesterLab](https://www.pentesterlab.com/): Hands-on training for penetration testers.
- [PortSwigger Web Security Academy](https://portswigger.net/web-security): Free security training from the makers of Burp Suite.
