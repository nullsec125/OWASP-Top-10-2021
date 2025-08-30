# Server-side Template Injection (SSTI)  

---

## Metadata  
- **OWASP Category (2021):** A03 Injections  
- **PortSwigger Link:** [Server-side template injection | Web Security Academy](https://portswigger.net/web-security/server-side-template-injection)  

---

## 💡 Concept  
- **What is it?**  
> When an attacker uses native template syntax to inject a malicious payload into a template – which is then executed server-side.  
> - Template engines generate web pages by combining fixed templates with volatile data.  

- **Impact:**  
> - **Confidentiality:** Access sensitive data, read files from the server, exfiltrate secrets.  
> - **Integrity:** Modify server-side logic, alter rendered pages, inject scripts into responses (stored/reflected XSS).  
> - **Availability:** Remote code execution (RCE) may enable full server takeover; denial-of-service through heavy template evaluation.  

---

## 🛠 Exploitation Notes  
- **Where to test:**  
> - Applications using template engines (Jinja2, Twig, Velocity, Smarty, Freemarker, etc.)  

- **Payloads**  
> - Simple test payloads:  
>   ```
>   {{7*7}} => 49 (Jinja2 / Twig)  
>   ${7*7} => 49 (Velocity, Freemarker)  
>   <%= 7*7 %> => 49 (ESI, JSP)  
>   ```  

---

## 🔍 Detection  
- Insert fuzz payloads like `{{7*7}}`, `${7*7}`, `<%=7*7%>` and look for evaluation results instead of literal text.  
- Error-based detection: Template errors often leak stack traces with engine names (like `Jinja2.exceptions.TemplateSyntaxError`).  
- Timing attacks: Use heavy operations (`{{range(10000000)|sum}}`) to cause noticeable delay.  
- Burp Suite Scanner (active scanning for SSTI).  
- Fuzz/Intruder with SSTI payload lists.  

---

## 🛡 Mitigation  
- Avoid dynamically rendering user input into templates.  
- Use safe APIs or restricted subsets with strict context separation.  
- Escape and validate user inputs properly.  

---

## Extras  
- **Cheat sheet / references:**  
  - [PayloadsAllTheThings – SSTI](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection)  

