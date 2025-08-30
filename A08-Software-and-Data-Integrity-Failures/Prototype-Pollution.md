# Prototype Pollution  

## Metadata  
- **OWASP Category (2021):** A08 Software and Data Integrity Failures  
- **PortSwigger Link:** What is prototype pollution? | Web Security Academy  

---

## 💡 Concept  
- **What is it?**  
> - A vulnerability in JavaScript applications where attackers can add or modify properties of the global `Object.prototype`.  
> - Because all objects inherit from this prototype, malicious changes can propagate application-wide.  

- **Impact**  
> - **Confidentiality:** Sensitive data leakage via altered object properties.  
> - **Integrity:** Tampering with critical application logic (ex: privilege escalation by modifying authorization checks).  
> - **Availability:** Application crashes or denial of service by overriding fundamental object properties.  

---

## ⚙️ Exploitation Notes  
- **Where to test:**  
> - Query parameters (`__proto__[admin]=true`)  
> - JSON request bodies (`{"__proto__":{"isAdmin":true}}`)  
> - Input passed into merge/deep-clone functions (`Object.assign`, `lodash.merge`, etc.)  

- **Payloads / Tricks used:**  
> - URL-based injection: `?__proto__[isAdmin]=true`  
> - JSON injection: `{"__proto__":{"isAdmin":true}}`  
> - Triggering a polluted sink if app logic checks `if (user.isAdmin)`, polluted prototype makes all objects evaluate as admin  
> - Gadget chains: Use polluted properties to call dangerous functions (like overriding `toString` or `constructor`)  

---

## 🔍 Detection  
> - Inspect parameters and request bodies for use of `__proto__`, `prototype`, or `constructor`.  
> - Send pollution payloads and check if new properties appear globally.  
> - Look for pollution sinks like JSON serialization, logging, or conditionals depending on object properties.  

---

## 🛡️ Mitigation  
> - Upgrade/patch vulnerable libraries (`lodash`, `jQuery`, etc.)  
> - Freeze/seal the `Object.prototype`.  
> - Use safe object creation methods (`Object.create(null)`).  
> - Sanitize and block suspicious keys (`__proto__`, `constructor`, `prototype`).  

---
