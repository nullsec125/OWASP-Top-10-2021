# A01 Broken Access Control

## 📑 Metadata
- **OWASP Category (2021):** [A01 Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)
- **PortSwigger Link:** [Access control vulnerabilities and privilege escalation | Web Security Academy](https://portswigger.net/web-security/access-control)

---

## 💡 Concept
- **What is it?**  
  Privilege Escalation via parameter-based access control methods, platform misconfiguration, or URL-matching discrepancies – or circumventing referrer headers, or geolocation mechanisms.
  - **Vertical Access:** Access to functionality not permitted.
  - **Horizontal Access:** Access to resources belonging to another user of that type.

- **Impact:**  
  - **Confidentiality:** Unauthorized users can gain access to sensitive data/restricted areas.  
  - **Integrity:** Attackers can alter/delete data outside permissions.  
  - **Availability:** Critical resources may be exposed, misused, and disabled.

---

## 🛠️ Exploitation Notes
- **Where to test:**  
  - Parameters: IDs in GET/POST requests (`/user?id=123 → try 124/343`).  
  - Headers: `X-User-Role: admin`.  
  - Cookies: Session IDs, JWT claims (`"role":"admin"`).  
  - Body: Hidden form fields (`isAdmin=true`).  
  - Endpoints: Admin panels, debug endpoints, file download/upload routes.

- **Payloads / Tricks used:**  
  - Modify object IDs to access other users’ records (`/invoice?id=10 → /invoice?id=20`).  
  - Replace JWT role claims (`"user" → "admin"`) or use unsigned tokens.  
  - Force-browse restricted URLs (`/admin`, `/config`, `/logs`).  
  - Replay/rotate session IDs.  
  - Abuse CORS misconfigurations to read protected endpoints.

---

## 🔎 Detection
- **How to identify in apps:**  
  - Try accessing restricted functions as a low-privilege user.  
  - Role-based checks missing on some endpoints.  
  - Test API calls directly (curl/Postman) bypassing the frontend UI.  
  - Check if session tokens remain valid after logout.  
  - Attempt direct object references (IDOR) with sequential or predictable IDs.  

- **Tools:**  
  - Burp Suite (Intruder for IDOR testing, Repeater for forced browsing).  
  - OWASP ZAP with authorization add-ons.

---

## 🛡️ Mitigation
- Adopt **Zero-Trust**, always verify.  
- Enforce **single application-wide mechanisms** for authorization checks.  
- At code level, **declare the access that is allowed for each resource**, and deny access by default.  
- Audit/test access controls to ensure they work as designed.  

---

## 📚 Extras
- **Cheat sheet / references:**  
  [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html)
