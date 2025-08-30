# Web Cache Poisoning

## Metadata
- **OWASP Category (2021):** A05 Security Misconfigurations
- **PortSwigger Link:** [Web cache poisoning | Web Security Academy](https://portswigger.net/web-security/web-cache-poisoning)

---

## 💡 Concept
- **What is it?**
> - An attack where an attacker manipulates the behavior of a web server and its cache so that harmful HTTP responses are cached and then served to other users.  
> - Instead of caching safe content, the cache stores a malicious response crafted by the attacker.

- **Impact**
> - **Confidentiality:** Can expose sensitive information if cached responses leak secrets.  
> - **Integrity:** Cache can be poisoned to store and serve altered/malicious responses to users.  
> - **Availability:** Legitimate users may be denied service or receive corrupted content.  
> - Real-world risks include XSS delivery at scale, user data exposure, phishing, or redirecting to malicious pages.

---

## 🛠 Exploitation Notes
- **Where to test:**
> - Headers (Host, X-Forwarded-Host, X-Forwarded-Scheme, etc.)
> - Parameters that affect cache keys
> - Resources that are likely cached (static files, API responses)

- **Tricks used**
> - Inject unkeyed inputs (headers/params not part of the cache key)
> - Trigger harmful backend responses that get cached

---

## 🔍 Detection
> - Look for discrepancies between what the cache stores and what the origin server sends.
> - Use Burp’s Param Miner to find unkeyed inputs.
> - Check if manipulated requests result in different cache storage.

---

## 🛡 Mitigation
> - Implement strong and consistent cache key definitions.
> - Avoid caching unkeyed or unsafe inputs (headers/parameters).
> - Only cache static, user-nonspecific content.
> - Use framework caching libraries correctly with security-aware defaults.

