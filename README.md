# BugBountyMastery

## 🚀 Introduction
This repository contains a comprehensive bug bounty methodology, designed for anyone interested in getting started or improving their skills in bug hunting. The methodology covers the entire process from reconnaissance to reporting vulnerabilities, with a focus on common tools, payloads, and techniques.

## 🧩 Table of Contents
1. [🔍 Reconnaissance](#1-reconnaissance)
    - [Subdomain Enumeration](#subdomain-enumeration)
    - [Service Identification](#service-identification)
    - [Port Scanning](#port-scanning)
    - [Fingerprinting](#fingerprinting)
2. [🛠️ Vulnerability Analysis](#2-vulnerability-analysis)
    - [Common Vulnerabilities](#common-vulnerabilities)
    - [Fuzzing & Directory Brute-forcing](#fuzzing--directory-brute-forcing)
    - [Sensitive Files and Configurations](#sensitive-files-and-configurations)
3. [💥 Exploitation](#3-exploitation)
    - [XSS (Cross-Site Scripting)](#xss-cross-site-scripting)
    - [SQL Injection](#sql-injection)
    - [Command Injection](#command-injection)
4. [📝 Reporting](#4-reporting)
    - [Report Structure](#report-structure)
    - [Tools for Documentation](#tools-for-documentation)
5. [💡 Common Payloads](#5-common-payloads)
6. [📚 Resources](#6-resources)

---

## 1. 🔍 Reconnaissance
**Purpose**: Gather information about the target to identify potential attack surfaces.

### Subdomain Enumeration
- **Sublist3r**: A tool to find subdomains using various sources like Google and VirusTotal.
    ```bash
    sublist3r -d example.com -o subdomains.txt
    ```

- **Amass**: A comprehensive open-source tool for network mapping and subdomain enumeration.
    ```bash
    amass enum -d example.com -o amass_subdomains.txt
    ```

- **Fierce**: A DNS reconnaissance tool for gathering information about subdomains and other DNS records.
    ```bash
    fierce --domain example.com
    ```

- **DNSdumpster**: A free online tool for finding subdomains, DNS records, and other related information.
    [Website - DNSdumpster](https://dnsdumpster.com/)

### Service Identification
- **Wappalyzer**: Identifies technologies in use on a website (e.g., PHP, WordPress, React).
- **WhatWeb**: A tool that identifies the technologies used by websites. It can identify web servers, CMS, and JavaScript frameworks.
    ```bash
    whatweb example.com
    ```

### Port Scanning
- **Nmap**: Scans for open ports and identifies services.
    ```bash
    nmap -sC -sV -iL active_hosts.txt -oN nmap_scan.txt
    ```

- **Shodan**: Provides a search engine for internet-connected devices, helping you identify vulnerable devices.
    [Website - Shodan](https://www.shodan.io/)

### Fingerprinting
- **WhatWeb**: Identifies web technologies, CMS, JavaScript frameworks, and more.
- **WhatWeb**: Detects the technologies used on a website, including the server and CMS.
    ```bash
    whatweb example.com
    ```

---

## 2. 🛠️ Vulnerability Analysis
**Purpose**: Identify weaknesses in the application's attack surfaces.

### Common Vulnerabilities
- **SQL Injection**: Automates the detection and exploitation of SQL injection vulnerabilities.
    ```bash
    sqlmap -u "https://example.com/page?parameter=value" --dbs
    ```

- **XSS**: Scans for XSS vulnerabilities and tests with various payloads.
    ```bash
    python3 xsstrike.py -u "https://example.com/search?q=test"
    ```

- **Command Injection**: Test if the application executes system commands via user input.
    ```bash
    ; ls -la
    ```

### Fuzzing & Directory Brute-forcing
- **Dirb**: Brute-forces directories and files on the server.
    ```bash
    dirb https://example.com /path/to/wordlist.txt -o directories.txt
    ```

- **Gobuster**: A tool for directory and file busting, also supports DNS subdomain brute-forcing.
    ```bash
    gobuster dir -u https://example.com -w /path/to/wordlist.txt
    ```

- **FFUF (Fuzz Faster U Fool)**: A fast web fuzzer that can find hidden endpoints.
    ```bash
    ffuf -u https://example.com/FUZZ -w /path/to/wordlist.txt
    ```

### Sensitive Files and Configurations
- **Nikto**: A web server scanner that detects vulnerabilities like outdated software, security misconfigurations, and more.
    ```bash
    nikto -h https://example.com
    ```

- **Retire.js**: Scans for vulnerable JavaScript libraries.
    ```bash
    retire --path /path/to/project
    ```

---

## 3. 💥 Exploitation
**Purpose**: Demonstrate the vulnerability and show its impact.

### XSS (Cross-Site Scripting)
- **Example Payload**:
    ```html
    <script>alert('XSS')</script>
    ```
    **Placement**: Form field, search bar, or URL parameter.  
    **Purpose**: Tests if JavaScript is executed.

### SQL Injection
- **Example Payload**:
    ```sql
    ' OR '1'='1' --
    ```
    **Placement**: Login form, URL parameter, or any user input field.  
    **Purpose**: Tests for unprotected SQL queries.

### Command Injection
- **Example Payload**:
    ```bash
    ; ls -la
    ```
    **Placement**: URL parameter, form field.  
    **Purpose**: Tests if system commands can be executed via user input.

---

## 4. 📝 Reporting
**Purpose**: Document findings clearly to help the development team fix the issue.

### Report Structure
- **Title**: [Type of vulnerability] in [target].
- **Summary**: A brief description of the issue.
- **Reproduction**: Step-by-step instructions to reproduce the bug.
- **Impact**: What could go wrong if the bug is exploited?
- **Suggested Fix**: How to resolve the bug?

### Tools for Documentation
- **Obsidian** / **Notion**: Note-taking tools for keeping track of findings.
- **OBS Studio**: Record evidence of vulnerabilities to demonstrate the steps involved.

---

## 5. 💡 Common Payloads

| Vulnerability Type   | Payload                                | Placement               | Purpose                                                   |
|----------------------|----------------------------------------|-------------------------|-----------------------------------------------------------|
| **XSS**              | `<script>alert('XSS')</script>`         | Search Field/Form       | Tests if JavaScript is executed.                          |
| **SQL Injection**    | `' OR '1'='1' --`                      | URL/Login Field         | Tests for unprotected SQL queries.                       |
| **Command Injection**| `; ls -la`                             | URL/Input Field         | Tests if system commands are executed.                    |
| **CSRF**             | `<img src="http://example.com/change?param=value">` | HTML                   | Tests if an unauthenticated change can be triggered.      |

---

## 6. 📚 Resources to keep yourself updated:

- [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings): A comprehensive list of useful payloads for various vulnerabilities.
- [Hacker101](https://www.hacker101.com/): Free security training resources by HackerOne.
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/): A series of best practice cheat sheets for various security topics.
- [Bugcrowd University](https://www.bugcrowd.com/bugcrowd-university/): Learn from Bugcrowd’s bug bounty platform and training courses.
- [PentesterLab](https://www.pentesterlab.com/): Hands-on training for penetration testers.
- [PortSwigger Web Security Academy](https://portswigger.net/web-security): Free security training from the makers of Burp Suite.
