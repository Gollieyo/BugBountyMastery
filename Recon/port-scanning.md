# 🔍 Port Scanning

## Purpose
Identify open ports and running services to locate potential vulnerabilities.

## Tools
1. **Nmap**:
    ```bash
    nmap -sC -sV -oN nmap_results.txt example.com
    ```

2. **Masscan**:
    ```bash
    masscan -p1-65535 --rate=1000 -oG masscan_results.txt example.com
    ```

## Tips
- Start with Nmap’s default scans, then use detailed scripts as needed.
- Verify suspicious ports with follow-up scans.

