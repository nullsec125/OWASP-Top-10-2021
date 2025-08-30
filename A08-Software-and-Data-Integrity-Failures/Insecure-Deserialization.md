# Insecure Deserialization  

## 📑 Metadata  
- **OWASP Category (2021):** A08 Software and Data Integrity  
- **PortSwigger Link:** [Insecure deserialization | Web Security Academy ](https://portswigger.net/web-security/deserialization) 

---

## 🌱 Concept  
- **What is it?**  
> - Serialization = converting objects into a storable/transmittable format (like byte streams, JSON, XML).  
> - Deserialization = reconstructing objects from serialized data.  
> - **Insecure deserialization = occurs when untrusted data is deserialized without validation, allowing attackers to manipulate serialized objects and influence application logic.**  

- **Impact**  
> - **Confidentiality:** Attackers may exfiltrate sensitive data via modified objects.  
> - **Integrity:** Data manipulation (tampering with objects, injecting arbitrary classes, exploiting logic flaws).  
> - **Availability:** Remote code execution (RCE), denial-of-service via malicious payloads.  

---

## ⚙️ Exploitation Notes  
- **Where to test:**  
> - Cookies storing serialized objects  
> - Hidden form fields  
> - API requests transmitting serialized payloads  
> - File uploads that may be parsed  

- **Tricks used:**  
> - Modify serialized data manually  
> - Exploit magic methods (`__wakeup, __destruct, __toString`) in PHP to trigger execution  
> - Inject arbitrary objects: Replace expected objects with attacker-controlled classes  
> - Gadget chains: Chain existing code fragments in libraries to reach RCE  
> - PHAR deserialization: Uploading PHAR archives to exploit unsafe file operations  

---

## 🔍 Detection  
> - Look for Base64, hex, or binary blobs in cookies, requests, or hidden fields.  
> - Modify serialized values and observe behavior (tamper test).  
> - PHP: `O:4:"User":2:{s:8:"username";s:5:"admin";}` structure is a red flag.  
> - Java: Presence of serialized object streams (`ac ed 00 05`) in traffic.  

---

## 🛡️ Mitigation  
> - Avoid deserializing untrusted data entirely.  
> - Implement integrity checks (HMAC/signing) for serialized data.  
> - Restrict classes allowed to be deserialized.  
> - Monitor for suspicious object structures in traffic.  

---

## 📚 Extras  
- **Cheat sheet / references:** [https://github.com/ambionics/phpggc?utm_source=chatgpt](https://github.com/ambionics/phpggc?utm_source=chatgpt)  

