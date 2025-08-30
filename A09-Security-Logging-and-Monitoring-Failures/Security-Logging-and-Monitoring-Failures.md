# A09 Insufficient Logging and Monitoring  

## Metadata  
- **OWASP Category (2021):** A09 Security Logging and Monitoring Failures  

---

## 💡 Concept  
- **What is it?**  
> Failure to properly log security-relevant events, or insufficient monitoring of those logs, prevents timely detection of attacks or breaches.  

- **Impact / Why it matters:**  
> - **Confidentiality:** Breaches go undetected, leading to prolonged data theft.  
> - **Integrity:** Malicious changes occur without audit or traceability.  
> - **Availability:** Attacks persist longer, extending downtime.  

---

## ⚙️ Exploitation Notes  
- **Where to test:**  
> - Login failures, privilege changes, API abuse, access to sensitive data.  
> - Check whether alerts are triggered during brute-force, SQLi, or RCE attempts.  

- **Tricks used:**  
> - Repeated failed logins.  
> - SQLi/XSS attempts with no alerts triggered.  
> - API abuse (rate-limiting bypass).  

---

## 🔍 Detection  
> - Simulate common attacks and observe if alerts/log entries exist.  
> - Review log files for completeness (user, IP, timestamps, context).  
> - SIEM Solutions (Splunk, ELK, etc).  
> - IDS/IPS with logging integrations.  

---

## 🛡️ Mitigation  
> - Ensure security events are logged (auth failures, privilege escalations, sensitive operations).  
> - Store logs in a centralized, tamper-proof system.  
> - Use alerting pipelines (SIEM/SOC).  
> - Correlate anomalies across systems.  
> - Regularly test logging coverage with Red/Blue team exercises.  

---

