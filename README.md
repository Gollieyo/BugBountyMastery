# BugBountyMastery

## 🚀 Introduction
This repository contains a comprehensive bug bounty methodology, designed for anyone interested in getting started or improving their skills in bug hunting. The methodology covers the entire process from reconnaissance to reporting vulnerabilities, with a focus on common tools, payloads, and techniques.

## 🧩 Table of Contents
1. [Reconnaissance](#1-reconnaissance)
2. [Vulnerability Analysis](#2-vulnerability-analysis)
3. [Exploitation](#3-exploitation)
4. [Reporting](#4-reporting)
5. [Common Payloads](#5-common-payloads)
6. [Resources](#6-resources)

## 1. Reconnaissance
**Purpose**: Gather information about the target to identify potential attack surfaces.

### Steps to Follow:
- Identify subdomains and live hosts.
- Analyze services and technologies in use (e.g., CMS, frameworks).
- Scan for open ports and services.

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

### Key Tips:
- Save all results from your reconnaissance as they will be needed in later stages.
- Be mindful of staying within the "scope" defined by the target.

## 2. Vulnerability Analysis
**Purpose**: Identify weaknesses in the application's attack surfaces.

### Steps to Follow:
- Manually test for common vulnerabilities.
- Perform fuzzing to find hidden endpoints or parameters.
- Validate and confirm vulnerabilities.

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

## 3. Exploitation
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

## 4. Reporting
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

## 5. Common Payloads

| Vulnerability Type | Payload                                | Placement               | Purpose                                                   |
|--------------------|----------------------------------------|-------------------------|-----------------------------------------------------------|
| **XSS**            | `<script>alert('XSS')</script>`         | Search Field/Form       | Tests if JavaScript is executed.                          |
| **SQL Injection**  | `' OR '1'='1' --`                      | URL/Login Field         | Tests for unprotected SQL queries.                       |
| **Command Injection** | `; ls -la`                          | URL/Input Field         | Tests if system commands are executed.                    |
| **CSRF**           | `<img src="http://example.com/change?param=value">` | HTML                   | Tests if an unauthenticated change can be triggered.      |

## 6. 📚 Resources to keep yourself updated:

- [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings): A comprehensive list of useful payloads for various vulnerabilities.
- [Hacker101](https://www.hacker101.com/): Free security training resources by HackerOne.

