# 💡 Common Payloads

| Vulnerability Type     | Payload                                | Placement               | Purpose                                                   |
|------------------------|----------------------------------------|-------------------------|-----------------------------------------------------------|
| **XSS**                | `<script>alert('XSS')</script>`         | Search Field/Form       | Tests if JavaScript is executed.                          |
| **SQL Injection**      | `' OR '1'='1' --`                      | URL/Login Field         | Tests for unprotected SQL queries.                       |
| **Command Injection**  | `; ls -la`                             | URL/Input Field         | Tests if system commands are executed.                    |
| **CSRF**               | `<img src="http://example.com/change?param=value">` | HTML                   | Tests if an unauthenticated change can be triggered.      |

