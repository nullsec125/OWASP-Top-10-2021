# HTTP Host Header Attacks  

## Metadata  
- **OWASP Category (2021):** A05 Security Misconfigurations  
- **PortSwigger Link:** [HTTP Host header attacks | Web Security Academy](https://portswigger.net/web-security/host-header)  

---  

## 🌿 Concept  
> -  Exploits vulnerable handling of the `Host` header in HTTP requests.  
> -  The header is meant to specify the domain name of the server being accessed, but if the application trusts this value without validation, attackers can manipulate it for malicious purposes.  

**Impact:**  
> - Cache poisoning (store attacker-controlled content in cache).  
> - Password reset poisoning (malicious links sent to users).  
> - Web cache deception and internal routing bypass.  
> - Security controls bypass (SSL/TLS misrouting, access control evasion).  
> - In extreme cases, account takeover and full compromise of web applications.  

---  

## 🛠 Exploitation Notes  
**Where to test:**  
> - Any app relying on `Host` header for routing, password reset links, or absolute URL generation.  
> - Virtual hosting setups, reverse proxies, and load balancers.  
> - Login portals, reset-password workflows, or anywhere absolute links are generated.  

**Tricks used:**  
> - Inject duplicate Host headers.  
> - Use X-Forwarded-Host, X-Host, or proxy headers.  

---  

## 🔍 Detection  
> - Observe generated absolute URLs (e.g., in password reset emails, redirects, or canonical headers).  
> - Test with modified `Host` headers and check if reflected in responses.  
> - Check for cache poisoning indicators by injecting unusual host strings and seeing persistence.  
> - Burp Suite scanner (`Host header` injection module).  

---  

## 🛡 Mitigation  
> - Avoid using `Host` header for security-critical logic.  
> - Use framework-provided server variables instead of raw `Host`.  
> - Whitelist allowed domains.  
>- Validate `Host` header strictly against expected values.  

