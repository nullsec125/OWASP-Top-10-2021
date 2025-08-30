# Path Traversal

## Metadata
- **OWASP Category (2021):** A05 Security Misconfigurations
- **PortSwigger Link:** [What is path traversal, and how to prevent it? | Web Security Academy](https://portswigger.net/web-security/file-path-traversal)

---

## 💡 Concept
- **What is it?**
> Allows attackers to manipulate file/directory paths to access files outside the intended web root.  
> By using sequences like `../`, attackers can move up the directory tree and read arbitrary files on the server.

- **Impact**
> - **Confidentiality:** Access sensitive files like `/etc/passwd`, application configs, or credentials.  
> - **Integrity:** Attackers may modify or overwrite files if the application allows write access.  
> - **Availability:** Critical file deletion or corruption may cause denial of service.

---

## 🛠 Exploitation Notes
> - **Where to test**
> - Parameters in URLs that specify filenames ( `?file=report.pdf` ).
> - Download endpoints ( `/download?file=` ).
> - Image retrieval functions.
> - File upload + retrieval combinations.

- **Payloads / Tricks used:**
> - Basic traversal: `../../../../etc/passwd`
> - Windows traversal: `..\..\..\..\boot.ini`
> - URL encoding to bypass filters: `%2e%2e%2f`, `%2e%2e/`, `%252e%252e%252f`, `%c0%ae%c0%ae%c0%afetc/passwd`
> - Null byte injection (legacy): `../../../../etc/passwd%00.png`

---

## 🔍 Detection
> - Look for parameters that reference files ( `?file=` ).
> - Try adding traversal sequences and check for file content leaks.
> - Error messages referencing system paths are a strong indicator.
> - Use Burp Repeater/Intruder to fuzz payloads.
- Burp Scanner

---

## 🛡 Mitigation
> - Avoid using user input directly in filesystem calls.
> - Use allowlists of permitted files.
> - Resolve and canonicalize paths, then enforce that they stay within intended directories.
> - Strip traversal sequences before processing.

