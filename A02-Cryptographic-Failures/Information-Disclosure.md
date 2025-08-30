# Information Disclosure

---

## Metadata
- **OWASP Category (2021):** A02 Cryptographic Failures (mainly)  
- **PortSwigger Link:** [Information disclosure vulnerabilities | Web Security Academy](https://portswigger.net/web-security/information-disclosure)

---

## 💡 Concept
- **What is it?**  
> When an application unintentionally exposes sensitive details through responses, error messages, or misconfigurations.  
> These details may not be directly harmful on their own but can provide attackers with clues to escalate attacks.

- **Impact:**  
> - **Confidentiality:** Exposure of PII, credentials, tokens, API keys, or internal system details  
> - **Integrity:** Leaked information can help craft more effective injection or logic attacks  
> - **Availability / Exploitation:** May enable account takeover, privilege escalation, or chaining with other vulnerabilities  

---

## 🛠 Exploitation Notes
- **Where to test:**  
> - HTTP response bodies (error messages, comments)  
> - HTTP headers (server banners, debug info, X-Powered-By)  
> - Directory listings on web servers  
> - JavaScript files, API responses, or backup files exposed  
> - robots.txt, .git directories  

- **Tricks used:**  
> - Trigger verbose error messages by manipulating parameters  
> - Look for sensitive comments in HTML/JavaScript  
> - Directory traversal to find backup/config files  
> - Use wordlists to brute-force hidden files/folders  

---

## 🔍 Detection
> - Manual inspection of server responses and error handling  
> - Test forced browsing (guess hidden URLs, backups)  
> - Monitor JavaScript and API responses for hardcoded tokens or keys  
> - Burp Suite Scanner (Information disclosure issues)  
> - Directory Buster / FFUF for directory and file enumeration  
> - Secret scanning tools (TruffleHog, Gitleaks) for exposed secrets  

---

## 🛡 Mitigation
> - Suppress detailed error messages in production  
> - Move hardcoded secrets in source code to secure storage (vaults, env configs)  
> - No sensitive data exposure in comments, API keys, or misused configs  
> - Enforce strict file permissions (no public access to backups/logs)  
