# CORS (Cross-Origin Resource Sharing) Attacks

## Metadata
- **OWASP Category (2021):** A05 Security Misconfigurations
- **PortSwigger Link:** [What is CORS (cross-origin resource sharing)? Tutorial & Examples | Web Security Academy](https://portswigger.net/web-security/cors)

---

## 💡 Concept
- **What is it?**
> CORS is a browser security mechanism that allows controlled access to resources across different origins. It relaxes the Same-Origin Policy by allowing servers to specify which origins are permitted to make cross-domain requests.  
> * Misconfigurations can lead to unauthorized access and data exfiltration.

- **Impact**
> - **Confidentiality:** Attackers can steal sensitive information (cookies, tokens, responses) if CORS is misconfigured.  
> - **Integrity:** Malicious websites can tamper with or manipulate cross-origin requests.  
> - **Availability:** Exploiting poorly configured CORS may allow service abuse, DoS through resource misuse, or breaking HTTPS protections.

---

## 🛠 Exploitation Notes
- **Where to test:**
> - HTTP request/response headers: `Origin`, `Access-Control-Allow-Origin`, `Access-Control-Allow-Credentials`
> - Browser interactions with APIs (XHR, Fetch, AJAX)
> - Authorization tokens/cookies with cross-origin requests

- **Tricks used**
> - Origin: `https://evil.com` → if server responds with: `Access-Control-Allow-Origin: https://evil.com` → Misconfigured.
> - Inject partial or malformed values to bypass filters (e.g., `null`, regex-based origin matching).

---

## 🔍 Detection
> - Inspect server responses for permissive headers (`Access-Control-Allow-Origin: *` or reflecting input)  
> - Check if `Access-Control-Allow-Credentials: true` is set with a wildcard  
> - Look for internal endpoints that unnecessarily expose data cross-origin  
- Burp Suite Pro Scanner  

---

## 🛡 Mitigation
> - Only use whitelisted origins in CORS configuration (explicit allowlists).  
> - Never use `Access-Control-Allow-Origin: *` with sensitive endpoints.  
> - Do not enable `Access-Control-Allow-Credentials` unless strictly necessary.  
> - Avoid reflecting arbitrary origins dynamically.  
> - Restrict sensitive APIs to same-origin.  
---

