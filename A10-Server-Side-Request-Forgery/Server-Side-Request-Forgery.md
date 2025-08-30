# A10 Server-Side Request Forgery  

## Metadata  
- **OWASP Category (2021):** A10 Server-Side Request Forgery  
- **PortSwigger Link:** [What is SSRF (Server-side request forgery)? Tutorial & Examples | Web Security Academy](https://portswigger.net/web-security/ssrf)  

---

## 💡 Concept  
- **What is it?**  
> - Allows an attacker to cause a server-side application to make requests to an unintended location.  
> - Exploiting this can create a connection to internal-only services within the organization’s infrastructure.  

- **Impact:**  
> - **Confidentiality:** Access internal systems and steal sensitive data (e.g., cloud metadata, admin panels).  
> - **Integrity:** Abuse internal services to perform unauthorized actions.  
> - **Availability:** Disrupt or exhaust internal services, causing denial of service.  

---

## ⚙️ Exploitation Notes  
- **Where to test:**  
> - Inputs that fetch remote resources (`/fetch?url=`).  
> - User-supplied features (file upload → remote image), PDFs.  
> - Headers (Referer, XML, DOCX) with embedded URLs.  

- **Payloads / Tricks used:**  
> - `http://localhost/admin` (bypass localhost restrictions).  
> - `http://127.0.0.1:80/` (loopback).  
> - `http://[::1]/` (IPv6 loopback).  
> - `http://169.254.169.254/latest/meta-data/` (cloud metadata endpoint).  
> - `http://internal-service/admin` (bypass internal access controls).  

- **Filter bypass techniques:**  
> - Alternate IP representations: `127.0.0.1`, `2130706433`, `017700000001`.  
> - URL encoding / case variations.  
> - Obfuscation via:  
>   - Decimal IP: `http://2130706433/`  
>   - Octal IP: `http://017700000001/`  
>   - Hexadecimal IP: `http://0x7f000001/`  
>   - DNS rebinding / wildcards.  

- **Exfiltration:**  
> - Open redirects to external URLs → internal domain then redirect externally.  
> - Blind SSRF: Trigger internal service that detects with DNS/HTTP callbacks.  

---

## 🔍 Detection  
> - Send payloads testing URL for file references.  
> - Test with alternate encodings, URL schemes (`file://`, `ftp://`, `dict://`).  
> - Monitor server-side errors (timeouts, error messages, stack traces).  
> - Burp Collaborator for blind SSRF detection.  

---

## 🛡️ Mitigation  
> - Avoid fetching remote URLs directly from user input.  
> - Use safe APIs (language libraries instead of system URL calls).  
> - Enforce strict allowlists (domain, IPs).  
> - Block access to internal IP ranges (loopback: `127.0.0.1`, `::1`, `169.254.*`, etc).  

---

## Extras  
- **Cheat sheet / references:** [SSRF Cheat Sheet | OWASP](https://portswigger.net/web-security/ssrf/ssrf-cheat-sheet)  

