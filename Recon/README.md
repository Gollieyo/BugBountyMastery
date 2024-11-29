# 🔍 Reconnaissance

**Purpose**: Gather information about the target to identify potential attack surfaces.

## Steps to Follow:
- Identify subdomains and live hosts.
- Analyze services and technologies in use (e.g., CMS, frameworks).
- Scan for open ports and services.
- **Identify DNS records**: DNS records may provide additional insights into the infrastructure.
- **Fingerprint the Web Server**: Find server software, version, and potential vulnerabilities.

## Tools:
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

- **Amass**: A comprehensive open-source tool for network mapping and subdomain enumeration.
    ```bash
    amass enum -d example.com -o amass_subdomains.txt
    ```

- **Shodan**: Provides a search engine for internet-connected devices, helping you identify vulnerable devices.

- **WhatWeb**: A tool that identifies the technologies used by websites. It can identify web servers, CMS, and JavaScript frameworks.

## Key Tips:
- Save all results from your reconnaissance as they will be needed in later stages.
- Be mindful of staying within the "scope" defined by the target.
