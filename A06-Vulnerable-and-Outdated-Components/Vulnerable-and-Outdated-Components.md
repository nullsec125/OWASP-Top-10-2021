# A06 Using Components with Known Vulnerabilities  

## Metadata  
- **OWASP Category (2021):** A06 Vulnerable and Outdated Components  

---

## 💡 Concept  
- **What is it?**  
> Applications rely on frameworks, libraries, OS packages, and other components.  
> When these are outdated or have known vulnerabilities, attackers can exploit them even if your custom code is secure.  

- **Impact**  
> - **Confidentiality:** Exploited flaws can leak sensitive data.  
> - **Integrity:** Attackers can modify code or data via known vulnerabilities.  
> - **Availability:** Outdated components may enable DoS or service outages.  

---

## ⚙️ Exploitation Notes  
- **Where to test:**  
> - Look at server banners, error messages, exposed version info.  
> - Exploit PoCs for known CVEs.  

- **Payloads / Tricks used:**  
> - Depends on specific CVE exploitation).  

---

## 🔍 Detection  
> - Version disclosure in headers or error messages.  
> - Dependency audit tools (npm audit, pip-audit, OWASP Dependency-Check).  
> - CVE databases and security advisories.  

---

## 🛡️ Mitigation  
> - Regularly patch and update frameworks/libraries.  
> - Use trusted registries and verify integrity of packages.  
> - Remove unused dependencies.  

