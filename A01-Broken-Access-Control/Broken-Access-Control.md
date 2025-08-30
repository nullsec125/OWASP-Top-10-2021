# Broken Access Control  

- **OWASP Category (2021):** A01 Broken Access Control
- **PortSwigger Link:** [Access control vulnerabilities and privilege escalation | Web Security Academy](https://portswigger.net/web-security/access-control)  

---

## 💡 Concept  

- **What is it?**  
> Privilege Escalation via parameter-based access control methods, platform misconfiguration, or URL-matching discrepancies – or circumventing referrer headers, or geolocation mechanisms.  
>  
> - Vertical = Access to functionality not permitted  
> - Horizontal = Access to resources belonging to another user of that type.  

- **Impact:**  
> - Confidentiality: Unauthorized users can gain access to sensitive data/restricted areas.  
> - Integrity: Attackers can alter/delete data outside their permissions.  
> - Availability: Critical resources may be exposed, misused, and disabled.  

---

## ⚙ Exploitation Notes  

- **Where to test:**  
> - Parameters: IDs in GET/POST requests (`/user?id=123 → try 124/343`).  
> - Headers: `X-User-Role: admin`.  
> - Cookies: Session IDs, JWT claims (`"role":"admin"`).  
> - Body: Hidden form fields (`isAdmin=true`).  
> - Endpoints: Admin panels, debug endpoints, file download/upload routes.  

- **Payloads / Tricks used:**  
> - Modify object IDs → access other users' records (`/invoice/101` → `/invoice/102`).  
> - Replace JWT role claims (`"user" → "admin"`) or use unsigned tokens.  
> - Force-browse restricted URLs (`/admin`, `/config`, `/logs`).  
> - Replay/Reuse session IDs.  
> - Abuse CORS misconfigurations to read protected endpoints.  

---

## 🔍 Detection  

- **How to identify in apps:**  
> - Try accessing restricted functions as a low-privilege user.  
> - Look for role-based checks missing on sensitive endpoints.  
> - Test API calls directly (curl/Postman) bypassing the UI.  
> - Check if session tokens remain valid after logout.  
> - Attempt direct object reference (IDOR) with sequential or predictable IDs.  
 - Burp Suite (Intruder for IDOR testing, Repeater for forced browsing).  
 - OWASP ZAP with authorization add-ons.  

---

## 🛡 Mitigation  

- **Developer-side fixes:**  
> - Zero-Trust, always verify.  
> - Single application-wide mechanism for enforcing access controls.  
> - At the code level, declare the access that is allowed for each resource, and deny access by default.  
> - Audit/Test access controls to ensure they work as designed.  

- **Defender-side fixes:**  
> - Monitoring, WAF rules, anomaly detection.  

---

## Extras  

- **Cheat sheet / references:** [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html)  
