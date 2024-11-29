
# Directory Enumeration

![License](https://img.shields.io/github/license/Gollieyo/BugBountyMastery) ![Last Commit](https://img.shields.io/github/last-commit/Gollieyo/BugBountyMastery) ![Version](https://img.shields.io/github/v/release/Gollieyo/BugBountyMastery)

## Purpose

Directory enumeration is an essential step in the reconnaissance phase of bug bounty hunting. It involves uncovering hidden directories and files on a target web server. These directories might contain sensitive information, misconfigured files, or even functionalities that developers intended to keep private. Proper directory enumeration can reveal new attack surfaces that lead to potential vulnerabilities.

---

## Tools

Here are two powerful tools for directory enumeration:

### 1. Gobuster
![Gobuster](https://img.shields.io/badge/Gobuster-Tool-blue)

Gobuster is a fast and efficient brute-force tool for discovering directories and files on web servers. It supports multithreading and works well with wordlists for targeted discovery.

#### Installation:
To install Gobuster on Debian-based systems:
```
sudo apt install gobuster
```

#### Basic Usage:
The basic syntax to run Gobuster is:
```
gobuster dir -u <URL> -w <wordlist>
```

#### Key Features:
- Multithreaded for faster scans.
- Support for file extension testing using the `-x` flag.
- Proxy support for anonymization or traffic monitoring.

---

### 2. FFUF (Fuzz Faster U Fool)
![FFUF](https://img.shields.io/badge/FFUF-Tool-yellow)

FFUF is another excellent tool for directory brute-forcing. It's known for its flexibility and speed, with powerful support for customized fuzzing.

#### Installation:
To install FFUF on Debian-based systems:
```
sudo apt install ffuf
```

#### Basic Usage:
The basic syntax to run FFUF is:
```
ffuf -u http://example.com/FUZZ -w /path/to/wordlist
```

#### Key Features:
- Fuzzing flexibility with placeholders like `FUZZ` for directory or file discovery.
- HTTP request customization for headers, cookies, etc.
- Support for filtering results by HTTP status codes, word count, or regex patterns.

---

## Tips

1. **Choose the Right Wordlist:**
   Your choice of wordlist can significantly impact the results. Some excellent resources include:
   - [SecLists - Web Content](https://github.com/danielmiessler/SecLists/tree/master/Discovery/Web-Content)
   - `/Discovery/Web-Content/common.txt`
   - `/Discovery/Web-Content/directory-list-2.3-medium.txt`

2. **Use File Extension Brute-Forcing:**
   Many web servers hide critical files by using extensions like `.php`, `.html`, `.txt`, or `.bak`. Use tools that allow extension testing to discover these.

   Example with Gobuster:
   ```
   gobuster dir -u http://example.com -w /path/to/wordlist.txt -x php,html,txt
   ```

3. **Combine Directory Enumeration with Other Tools:**
   Use tools like the `Wayback Machine` or `gau` (GetAllURLs) to gather historical URLs and directories, then use these as input for brute-forcing.

4. **Avoid Overloading Servers:**
   Respect the server's capacity by keeping thread counts reasonable (e.g., `-t 10`) and avoiding scans during peak hours.

5. **Monitor Your Traffic:**
   Route your requests through a proxy like Burp Suite or OWASP ZAP to analyze the server’s responses and find patterns that hint at hidden directories.

6. **Check Robots.txt and Sitemap.xml:**
   Before brute-forcing, look for these files to gain insight into the server’s structure:
   ```
   curl http://example.com/robots.txt
   curl http://example.com/sitemap.xml
   ```

---

## References

- [Gobuster GitHub Repository](https://github.com/OJ/gobuster)
- [FFUF GitHub Repository](https://github.com/ffuf/ffuf)
- [SecLists Wordlists](https://github.com/danielmiessler/SecLists)
